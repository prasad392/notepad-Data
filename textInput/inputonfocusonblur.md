
here the 'onfocus' means when the user focuses or clicks the input.

here the 'onBlur' means that the user not focuses the input.

const [msg,setMsg] = usestate('')

    <TextInput
        style={styles.input}
        placeholder="Enter name....."
        placeholderTextColor={"#000"}
        value={task.name}
        onChangeText={txt=>setTask(prev=>({...prev,name:txt}))}
        onFocus={()=>setMsg('input is focused')}
        onBlur={()=>setMsg('input is blur')}
        />
