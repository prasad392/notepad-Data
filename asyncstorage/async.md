
AsyncStorage:-

which uses to store the small data.
string key-value pairs of data.

=> npm install @react-native-async-storage/async-storage

=> import AsyncStorage from '@react-native-async-storage/async-storage';

to save the data in the local storage as

const handleSave = async()=>{
    const existing = await AsyncStorage.getItem('mytasks')
    const mytasks = existing ? JSON.parse(existing) : [];
    mytasks.push(task)
    await AsyncStorage.setItem('mytasks',JSON.stringify(mytasks))
    setTask('')
  }

to delete the data in local storage

const handleDelUser=async(item : string)=>{
    const stored = await AsyncStorage.getItem('mytasks');
    if(stored){
      const mytasks = JSON.parse(stored).filter((t : string)=>t !== item)
      await AsyncStorage.setItem('mytasks',JSON.stringify(mytasks))
      setUsers(mytasks)
    }
  }

to print the data in the page as,

const getUsers =async()=>{
    try{
      const storedUser = await AsyncStorage.getItem('mytasks')
      if(storedUser){
        setUsers(JSON.parse(storedUser))
        console.log(storedUser)
        console.log(JSON.parse(storedUser))
      }
    }
    catch(err){
      console.log(err)
    }
  }

useEffect(()=>{
    getUsers()
  },[])



// to add the data in the localstorage as the array of objects

[{ name: 'prasad', age: '20' }, { name: 'rama', age: '25' }]

// first we have to set the type for that that the object create then

type taskItem ={
  name: string;
  age: string;
}

// now create the state variable for that
const [task,setTask] = useState<taskItem>({
    name: '',
    age: '',
  })

here are the two inputs that can be useful for the enter use data.

    <TextInput
    style={styles.input}
    value={task.name}
    onChangeText={(txt)=>setTask(prev=>({...prev,name: txt}))}
    placeholder="name"
    />

    <TextInput
    style={styles.input}
    value={task.age}
    onChangeText={(txt)=>setTask(prev=>({...prev,age:txt}))}
    placeholder="age"
    />

// now we have to create the function to save the details on the local storage.

const handleSave =async()=>{
    const existing = await AsynStorage.getItem('mytasks')
    const mytasks = existing ? JSON.parse(existing) : [];
    mytasks.push(task)
    await AsyncStorage.setItem('mytasks',JSON.stringify(mytasks));
}

// to retreive the local data in the another component like,

in that component first we have to add the type for the state variable as,

type taskItem ={
  name: string;
  age: string;
}

const [users,setUsers] = usestate<taskItem[]>([])

const getUsers = async()=>{
    const stored = AsyncStorage.getItem('mytasks');
    if(stored){
        setUsers(JSON.parse(stored))
    }
}

useEffect(()=>{
    getUsers()
},[])

// now we can print the data by use flatlist

    <FlatList
    data={users}
    keyExtractor={item=>item.name.toString()}
    renderItem={({item})=>(
      <View>
        <Text> {item.name} </Text>
        <Text style={{fontSize:24}} onPress={()=>handleDelUser(item.name)}> Del</Text>
      </View>
    )}
    />

 // now we have to delete the object by using the name as,

const handleDelUser = async(item : string)=>{
    const stored = await AsyncStorage.getItem('mytasks');
    if(stored){
        const mytasks :taskItem[] = JSON.parse(stored);
        const updatedTasks = mytasks.filter(task=>task.name !== item)
        await AsynStorage.setItem('mytasks',JSON.stringify(updatedTasks))
        setUsers(updatedtasks)
    }
}