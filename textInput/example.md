
  import React, { useRef, useState } from 'react';
  import {
    View,
    TextInput,
    Animated,
    StyleSheet,
    KeyboardAvoidingView,
    Platform,
    ScrollView,
  } from 'react-native';

  const AnimatedInput = ({ label, value, onChangeText }) => {
    const anim = useRef(new Animated.Value(value ? 1 : 0)).current;

    const handleFocus = () => {
      Animated.timing(anim, {
        toValue: 1,
        duration: 200,
        useNativeDriver: false,
      }).start();
    };

    const handleBlur = () => {
      Animated.timing(anim, {
        toValue: value ? 1 : 0, // keep label up if there's text
        duration: 200,
        useNativeDriver: false,
      }).start();
    };

    return (
      <View style={styles.inputBox}>
        <Animated.Text
          style={{
            position: 'absolute',
            left: 45,
            top: anim.interpolate({ inputRange: [0, 1], outputRange: [40, 8] }),
            fontSize: anim.interpolate({ inputRange: [0, 1], outputRange: [18, 16] }),
            color: '#fff',
            backgroundColor: '#3e3e3e',
            paddingHorizontal: 4,
            zIndex: 1000,
          }}
        >
          {label}
        </Animated.Text>
        <TextInput
          style={styles.input}
          value={value}
          onChangeText={onChangeText}
          onFocus={handleFocus}
          onBlur={handleBlur}
          placeholder=""
        />
      </View>
    );
  };

  export default function App() {
    const [task, setTask] = useState({ name: '', age: '', email: '', address: '' });

    return (
      <KeyboardAvoidingView
        style={{ flex: 1, backgroundColor: '#3e3e3e' }}
        behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
        keyboardVerticalOffset={80} // adjust if you have headers
      >
        <ScrollView contentContainerStyle={{ padding: 20 }}>
          <AnimatedInput
            label="Name"
            value={task.name}
            onChangeText={(txt) => setTask((prev) => ({ ...prev, name: txt }))}
          />
          <AnimatedInput
            label="Age"
            value={task.age}
            onChangeText={(txt) => setTask((prev) => ({ ...prev, age: txt }))}
          />
          <AnimatedInput
            label="Email"
            value={task.email}
            onChangeText={(txt) => setTask((prev) => ({ ...prev, email: txt }))}
          />
          <AnimatedInput
            label="Address"
            value={task.address}
            onChangeText={(txt) => setTask((prev) => ({ ...prev, address: txt }))}
          />
        </ScrollView>
      </KeyboardAvoidingView>
    );
  }

  const styles = StyleSheet.create({
    inputBox: {
      marginBottom: 20,
      borderBottomWidth: 1,
      borderColor: '#ccc',
      paddingVertical: 10,
    },
    input: {
      fontSize: 18,
      color: '#fff',
      paddingLeft: 45,
    },
  });
