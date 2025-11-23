the textinput value will always be take the 'string' value only.

when we take the array of the objects to be store as the,

type taskItem ={
    name: string;
    age: number;
}

const [tasks,setTasks] = usestate<taskItem>({
    name: '',
    age: 0,
})

    <TextInput
    value={tasks.age === 0 ? '' : String(tasks.age)}
    />

// this can be shows the when the input is 0 then the input be empty is omly.