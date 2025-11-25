    @tailwind base;
    @tailwind components;
    @tailwind utilities;

    @layer components {
        .screen {
            @apply flex-1 bg-slate-300;
        }
        .label{
            @apply text-slate-950 font-bold
        }
    }

here this @layer componets used for the customize the style..

if u need to toogle the screen for the boolean in all over the components u have to use the multiple screens,

    @layer components{
        .screen-dark{
            @apply bg-slate-800
        }
        .screen-lisght{
            @apply bg-slate-300
        }
    }
    <View className={darkMode ? "screen-dark" : "screen-light"} />
