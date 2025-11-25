
=> context api which uses to avoid the prop drilling.
    // global state management
    // creates the context obj that holds state and functions use in any components.

    context --> context for global state.
    provider --> providees data & wraps app
    ReactNode --> A typescript type represents anything react render(elements, frgaments etc...,)

    { children }: { children: ReactNode } :-
    “Take the children property from the props object, and ensure it is of type ReactNode.”

    // children is the special React prop that represents whatever you wrap inside your component.
    // {children} is destructuring the props object.

    ReactNode → Anything React can render: strings, numbers, JSX, fragments, arrays, etc.

    ==== array of the values are printing ====

    // AppProvider Appcontext wrap the componets

    import React, { createContext, ReactNode, useContext, useState } from 'react'

    type AppContextType ={
        usersData: string[];
        setUsersData: React.Dispatch<React.SetStateAction<string[]>>
    }

    export const  AppContext = createContext<AppContextType | undefined>(undefined);

    const AppProvider = ({children}:{children:ReactNode}) => {
        const [usersData,setUsersData] = useState<string[]>(['guest']);
    return (
        <AppContext.Provider value={{usersData,setUsersData}}>
            {children}
        </AppContext.Provider>
    )
    }

    export default AppProvider

    export const useUser = ()=>{
        const userContext = useContext(AppContext)
        if(!userContext){
            throw new Error('Eror exists')
        }
        return userContext;
    }

    // we have to add the data through input feilds from one component and display in another context API.

        const {usersData,setUsersData} = useUser()
        const [inputFeilds,setInputFeilds] = usestate('')

        <View style={styles.inputBox}>
            <TextInput
                style={styles.input}
                placeholder='Name'
                value={inputFeilds}
                onChangeText={(txt)=>setInputFeilds(txt)}
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
            const res = usersData.filter(nan=>nan !== item)
            setUsersData(res)
        }

        <FlatList
        data={usersData}
        keyExtractor={item=>(item.toString())}
        renderItem={({item})=>(
          <>
            <Text> {item} </Text>
            <Text style={{color:'red',fontSize:20}} onPress={()=>handleDel(item)}> Delete </Text>
          </>
        )}
        />