    // home component for update with input feilds

    const [loading,setLoading] = useState(true)

    const [inputs,setInputs] = useState({
        name:'',
    })

        <View
            className="w-[90%] h-[60] mx-auto rounded-lg mt-10"
            >
            <TextInput
            className="border border-2 w-[90%] mx-auto rounded-lg text-xl"
            placeholder="name"
            placeholderTextColor={"#000"}
            value={inputs.name}
            onChangeText={(txt)=>setInputs(prev=>({...prev,name:txt}))}
            />
        </View>
        
        <TouchableOpacity
        className="bg-yellow-300 border border-2 w-[80%] mx-auto rounded-lg mt-10 h-[60] items-center justify-center"
        onPress={()=>{
            dispatch({type:'ADD_USER',payload:inputs.name})
            setInputs(prev=>({...prev,name:''}))
        }}
        >
            <Text className="label-black text-xl font-bold"> Save </Text>
        </TouchableOpacity>