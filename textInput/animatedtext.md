
animated text is as the normal text but with the animation like opacity.

    const opacity = useRef(new Animated.Value(0)).current;

    useEffect(()=>{
        Animated.timing(opacity,{
            toValue: 1,
            duration: 3000,
            useNativeDriver: false,
        }).start()
    },[])

    <Animated.Text style={{opacity}}> hello world </Animated.Text>
