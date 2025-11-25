
=> npm i nativewind tailwindcss react-native reanimated react-native-safe-area-context

=> npx tailwindcss init

// now on file is cretaed the tailwind.config.css

    in that file add this

    /** @type {import('tailwindcss').Config} */
    module.exports = {
    content: ["./app/**/*.{js,jsx,ts,tsx}","./components/**/*.{js,jsx,tsx}"],
    presets:[require("nativewind/preset")],
    theme: {
        extend: {},
    },
    plugins: [],
    }

// create on file babel.config.js

    module.exports = function (api) {
        api.cache(true);
        return {
        presets: [
        ["babel-preset-expo", { jsxImportSource:
        "nativewind" }],
        "nativewind/babel"
        ],
        };
    };
// in the terminal run this

here we have create the one global.css file and add this

    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    
    // make sure that this .css file in the root folder means stack folder.

=> npx expo customize metro.config.js

// now one file metro.config.js is created in the folder project.

    // Learn more https://docs.expo.io/guides/customizing-metro
    const { getDefaultConfig } = require('expo/metro-config');
    const {withNativeWind} = require("nativewind/metro")
    /** @type {import('expo/metro-config').MetroConfig} */
    const config = getDefaultConfig(__dirname);

    module.exports = withNativeWind(config,{input: "./app/global.css"});

