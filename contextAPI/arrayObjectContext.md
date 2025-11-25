
    ===== array of the objects ====

    // AppProvider AppContext

        import React, { createContext, ReactNode, useContext, useState } from 'react'

        type userItem ={
            name : string;
            age: number;
        }

        type AppContextType ={
            usersData: userItem[];
            setUsersData: React.Dispatch<React.setStateAction<userItem[]>>
        }

        export const AppContext = createContext<AppContextType | undefined>(undefined);

        const AppProvider =({children}:{children:ReactNode})=>{
            const [userData,setUsersData] = usestate<userItem[]>([])
            return(
                <AppContext.Provider>
                    {children}
                </AppContext.Provider>
            )
        }
        export default AppProvider;

        export const useUser = ()=>{
            const user = useContext(AppContext);
            if(!user){
                throw new Error("error found")
            }
            return user;
        }

    // we have to add the data through input feilds from one component and display in another context API.

        import { useUser } from '@/src/context/appcontext';
        
        type userItem ={
            name : string;
            age: number;
        }

        const {usersData,setusersData} = useUser();

        const [inputFeilds,setInputFeilds] = useState<userItem>({
            name:'',
            age:0
        });

        <View style={styles.inputBox}>
          <TextInput
            style={styles.input}
            placeholder='Name'
            value={inputFeilds.name}
            onChangeText={(txt)=>setInputFeilds(prev=>({...prev,name:txt}))}
          />
        </View>
        <View style={styles.inputBox}>
            <TextInput
                style={styles.input}
                placeholder='Age'
                value={inputFeilds.age === 0 ? '' : String(inputFeilds.age)}
                onChangeText={(txt)=>setInputFeilds(prev=>({...prev,age:Number(txt)}))}
            />
        </View>
        <TouchableOpacity
            style={styles.continueBtn}
            onPress={()=>{
            setUsersData(prev=>[...prev,inputFeilds])
            }}
            >
            <Text style={{fontSize:22}}>Save</Text>
        </TouchableOpacity>

    // now to print the data in another component and delete the selected data

        const {usersData,setUsersData} = useUser();

        const handleDel=(item:string)=>{
            const res = usersData.filter(nan=>nan.name !== item)
            setUsersData(res)
        }

        <FlatList
        data={usersData}
        keyExtractor={item=>(item.toString())}
        renderItem={({item})=>(
          <>
            <Text> {item.name} </Text>
            <Text style={{color:'red',fontSize:20}} onPress={()=>handleDel(item.name)}> Delete </Text>
          </>
        )}
        />

