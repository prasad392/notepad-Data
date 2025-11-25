
firebase is the backend development storage that provides the authentication,cloud storage.

firetore is a NoSQL cloud database provided by firebase. it stores data in collections and documents.

collection => a group of documents.

document => a single record with key-value pairs.


=> In the firebase integratio we have the authentication and we have implement that.

// now open "firebase console" in browser and create a project

// in the left open the run --> authentication and click get started.

// click Email/Password and enable the Email/Password only.

// click the project overview and regiter the app (Android only/-). +Add

    --> to register the app

    ==> com.veggiesList [this may be the any url for the app].

    ==> click register and download the .json file 

    google-services (1).json this look like

// now open the app in that open the src folder and create a file "firebaseConfig.js" .

    => npm i firebase

    --> in that file need to mention this
    
    const firebaseConfig = {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
        projectId: "YOUR_PROJECT_ID",
        storageBucket: "YOUR_PROJECT_ID.appspot.com",
        messagingSenderId: "YOUR_SENDER_ID",
        appId: "YOUR_APP_ID"
    };

    // this is the firebase authentication building...

    import { initializeApp } from "firebase/app";
    import { getAuth } from "firebase/auth";

    const firebaseConfig ={
        apiKey: "AIzaSyB7BvB3vDSYGoaa_PQFE1decFxOjm-W8FQ",
        authDomain: "veggieslist-c54b8.firebaseapp.com",
        projectId: "veggieslist-c54b8",
        storageBucket: "veggieslist-c54b8.appspot.com"
        messagingSenderId: "995489796112"
        appId: "1:995489796112:android:de14e0f3149fa15aa3ba95"
    }
    const app = initializeApp(firebaseConfig)
    export const auth = getAuth(app)

    // if you want to store the credentials in the localstorage as the AsyncStorage like,

    import {initializeAuth,getReactNativePersistence} from "firebase/auth"
    import AsyncStorage from '@react-native-async-storage/async-storage';

    const app = initailize(firebaseConfig)
    export const auth = initializeAuth(app,{
        persistence: getReactNativePersistence(AsyncStorage)
    })

    // to view the data that stored in the local storage as,
    
    const showData =async()=>{
        const keys = await AsyncStorage.getAllKeys();
        console.log(keys)
    }
    useEffect(()=>{
        showData()
    })