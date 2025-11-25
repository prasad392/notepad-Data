
componets folder create file screencontainer.tsx

// components/ScreenContainer.tsx
    export default function ScreenContainer({ children, darkMode }: { children: React.ReactNode; darkMode: boolean }) {
        return (
            <View
            className={`flex-1 ${darkMode ? 'bg-slate-800' : 'bg-slate-300'}`}
            style={{ paddingTop: Platform.OS === 'android' ? StatusBar.currentHeight : 0 }}
            >
            {children}
            </View>
        );
    }

and use in the home or settings as the

    import ScreenContainer from "../components/ScreenContainer";

    const Home = () => (
    <ScreenContainer>
        <StatusBar barStyle="dark-content" />
        <Text>Home</Text>
    </ScreenContainer>
    );
