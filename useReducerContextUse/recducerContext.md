
    import AsyncStorage from "@react-native-async-storage/async-storage";
    import React, { createContext, ReactNode, useContext, useEffect, useReducer, useState } from "react";

    type StateType ={
        newUser: string[];
    }
    type ActionType =
        | {type: "ADD_USER"; payload: string}
        | {type: "DELETE_USER"; payload: string}

    const initialState:StateType = {
        newUser: [],
    }
    type AppContextType ={
        state: StateType;
        dispatch : React.Dispatch<ActionType>;
    }
    function appReducer(state:StateType, action:ActionType):StateType{
        switch(action.type){
            case 'ADD_USER':
                return {...state,newUser:[...state.newUser,action.payload]}
            case 'DELETE_USER':
                return {...state,newUser:state.newUser.filter(user=>user !== action.payload)}
            default:
                return state;
        }
    }
    export const AppContext = createContext<AppContextType | undefined>(undefined)

    export default function AppProvider({children}:{children:ReactNode}){
        const [state,dispatch] = React.useReducer(appReducer,initialState);
        useEffect(()=>{
            const loadData =async()=>{
                const stored = await AsyncStorage.getItem('users')
                if(stored){
                    const parsed = JSON.parse(stored)
                    parsed.forEach((user:string)=>{
                        dispatch({type:'ADD_USER',payload:user})
                    })
                }
            }
            loadData()
        },[])
        useEffect(()=>{
            const saveData = async()=>{
                await AsyncStorage.setItem('users',JSON.stringify(state.newUser))
            }
            saveData()
        },[state.newUser])
        return(
            <AppContext.Provider value={{state,dispatch}}>
                {children}
            </AppContext.Provider>
        )
    }

    export const useNewUser = ()=>{
        const context = useContext(AppContext);
        if(!context){
            throw new Error('error occured')
        }
        return context;
    }