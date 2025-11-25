
firestore that contains the database and we can add it in the database of ptoject

=> firestore database
=> create database 
=> collection id means that name 'users'
=> create the db by the documents

now to fetch the data in the app as the using " getDocs() or Onsnapshot() ".

the getDocs() which use to render only one time 
where the onsnapshot() uses for the real-time data updates and the component unmopunts.

=> getDocs()

    type userItem={
    id: string;
    age: number;
    name: string;
    email : string;
    location: string;
    mobile: string;
    }

    const [userdata,setUserdata] = useState<userItem[]>([])

    useEffect(()=>{
        const fetchUsers =async()=>{
        const querySnapshot = await getDocs(collection(db,'users'));
        const data:userItem[] = querySnapshot.docs.map(doc=>{
            const docData = doc.data() as userItem;
            return {...docData,id:doc.id}
        })
        setUserdata(data)
        }
        fetchUsers()
    },[])

=> Onsnapshot()

    import {collection, onSnapshot} from 'firebase/firestore'
    import {db} from '@/firebaseConfig'

    type userItem={
    id: string;
    age: number;
    name: string;
    email : string;
    location: string;
    mobile: string;
    }

    const [userdata,setUserdata] = useState<userItem[]>([])   

    useEffect(()=>{
        const unsubscribe = onSnapshot(collection(db,'users'),snapshot=>{
        const data: userItem[] = snapshot.docs.map(doc=>{
            const docData = doc.data() as userItem;
            return {...docData,id:doc.id}
        })
        setUserdata(data)
        })
        return unsubscribe;
    },[])

---- ------- ------ ------- -------- ------ 
    to add data in the data by the form as the
    =>addDoc()

        import { addDoc, collection } from 'firebase/firestore';
        import { db } from '@/firebaseConfig';

        type userItem={
            age: number;
            name: string;
            email : string;
            location: string;
            mobile: string;
        }
        const [formData,setFormData] = useState<userItem>({
            name:'',
            age: 0,
            email: '',
            location: '',
            mobile: '',
        })

        const handleContinue =async()=>{
            const {name,age,email,location,mobile} = formData;
            if(!name || !age || !email || !location || !mobile){
                Alert.alert("feilds are required...")
                return;
            }
            await addDoc(collection(db,'users'),{
                name: formData.name,
                age: Number(formData.age),
                email: formData.email,
                location: formData.location,
                mobile: formData.mobile
            })
            onClose();
            setFormData({name:'',age:0,location:'',mobile:'',email:''})
        }
------ ---- ------- -------- ---- ---------- ----- 
// delete the particular user

=> deleteDoc()

    import {doc} from 'firebase/firestore';

    const handleDel=async(id:string)=>{
        await deleteDoc(doc(db,'users',id))
    }

    <Text onPress={()=>handleDel(item.id)} style={{color:'red',fontSize:18,textAlign:'center'}}>Delete</Text>

