import AsyncStorage from '@react-native-async-storage/async-storage';
import { useEffect, useRef, useState } from "react";
import { Animated, Platform, StatusBar, StyleSheet, Text, TextInput, TouchableOpacity, View } from "react-native";

type taskItem ={
  name: string;
  age: number;
}

export default function Index() {
  const [focused,setFocused] = useState(false);
  const anim = useRef(new Animated.Value(0)).current;
  const [task,setTask] = useState<taskItem>({
    name: '',
    age: 0,
  })

  useEffect(()=>{
    Animated.timing(anim,{
      toValue: focused || task.name ? 1 : 0,
      duration: 200,
      useNativeDriver: false,
    }).start()
  },[focused,task.name])

  const handleSave = async ()=>{
    const existing = await AsyncStorage.getItem('mytasks')
    const mytasks = existing ? JSON.parse(existing) : [];
    mytasks.push(task)
    await AsyncStorage.setItem('mytasks',JSON.stringify(mytasks))
  }

  return (
    <View style={styles.container}>
      <StatusBar barStyle={'dark-content'}/>

        <Animated.Text
        style={{
          position:'absolute',
          left:30,
          top: anim.interpolate({inputRange: [0,1], outputRange: [72,52]}),
          fontSize: anim.interpolate({inputRange: [0,1],outputRange: [18,16]},),
          color: '#000',
          paddingHorizontal:1,
          zIndex:1,
          backgroundColor:'#fff'
        }}
        >Enter Name </Animated.Text>
        <TextInput
        style={[styles.input,{ borderColor: focused ? "#00bfff" : "#666" },]}
        placeholder=""
        placeholderTextColor={"#000"}
        value={task.name}
        onChangeText={txt=>setTask(prev=>({...prev,name:txt}))}
        onFocus={()=>setFocused(true)}
        onBlur={()=>setFocused(false)}
        />

        <TextInput
        style={styles.input}
        placeholder="Enter age....."
        placeholderTextColor={"#000"}
        value={task.age === 0 ? '' : String(task.age)}
        onChangeText={txt=>setTask(prev=>({...prev,age:Number(txt)}))}
        keyboardType="number-pad"
        />

        <TouchableOpacity
        style={styles.saveBtn}
        onPress={handleSave}
        >
          <Text style={{fontSize:20}}> Save </Text>
        </TouchableOpacity>
    </View>
  );
}
const styles = StyleSheet.create({
  container:{
    flex:1,
    backgroundColor:'#fff',
    paddingTop: Platform.OS === 'android' ? StatusBar.currentHeight : 0,
  },
  input:{
    borderWidth:2,
    borderColor:'#000',
    width:'90%',
    marginVertical:20,
    marginHorizontal:'auto',
    borderRadius:12,
    color:'#000'
  },
  saveBtn:{
    width:'90%',
    marginVertical:20,
    marginHorizontal:'auto',
    borderRadius:12,
    backgroundColor:'#ffd60a',
    height:40,
    justifyContent:'center',
    alignItems:'center'
  }
})