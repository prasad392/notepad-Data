
=> npm install @reduxjs/toolkit
=> npm install react-redux

state,actions,reducer,dispatch,selector.

// redux folder in the app.
// redux folder has one "store" file and "slices" folder.

    === store.js ===
    import { configureStore } from "@reduxjs/toolkit";
    import counterReducer from './slices/counterSlice';

    export const store = configureStore({
        reducer:{
            counter: counterReducer
        }
    })
    export type RootState = ReturnType<typeof store.getState>
    export type AppDispatch = typeof store.dispatch;

    // RootState, AppDispatch are the types that are used for globally.

    === slices/counterslice.ts ===
    
    import {createSlice} from '@reduxjs/toolkit';

    interface CounterState{
        value : number;
    }

    const initialState : CounterState = { value:0 };

    const CounterSlice = createSlice({
        name:'counter',
        initialState,
        reducers:{
            increment: (state) => {state.value+=1},
            decrement: (state)=>{state.value-=1},
            reset: (state)=>{state.value = 0}
        }
    })

    export const {increment,decrement,reset} = CounterSlice.actions;
    export default CounterSlice.reducer;

    // interface is also acts like the type ={}
        => CounterSlice.reducer is acts like counterReducer.
    
    === rootlayout.ts===
    
    import { store } from "@/redux/store";
    import { Stack } from "expo-router";
    import {Provider} from 'react-redux'

    export default function RootLayout() {
        return (
            <Provider store={store}>
                <Stack screenOptions={{headerShown:false}}>
                    <Stack.Screen name="(tabs)" options={{title:'Tabs'}}/>
                </Stack>
            </Provider>
        )
    }
