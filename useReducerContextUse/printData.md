    // ptoducts for print data

    const Products = () => 
    const {state,dispatch} = useNewUser()
    
        <View className='w-[90%] bg-slate-500 h-[70px] mx-auto rounded-lg mt-10 items-center justify-between flex-row'>
          <Text className='label-white text-3xl'> {item} </Text>
          <TouchableOpacity
          className='w-35 bg-red-500 items-center justify-center mr-10'
          onPress={()=>{
            dispatch({type:'DELETE_USER',payload:item})
          }}
          >
            <Text className='text-xl font-bold'> Delete </Text>
          </TouchableOpacity>
        </View>