# Animate Icon in Flutter

```dart
class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

// SingleTickerProviderStateMixin is a mixin that
// provides a single-tick animation controller.
class _HomeScreenState extends State<HomeScreen>
    with SingleTickerProviderStateMixin {
  // Define the animation object to animate the controller
  // and then assign the animation to the process argument of 
  // AnimatedIcon widget.
  late final AnimationController _controller;
  late final Animation<double> _animation;

  @override
  void initState() {
    // Create the animation controller widh 1 second of duration.
    // So the animated icon will take 1 second to animate and 1 seond
    // to reverse as well.
    _controller = AnimationController(
      vsync: this,
      duration: Duration(seconds: 1),
    );
    // Create the animation object with the value of 0.0 to 1.0.
    // This will control the process of animated icon.
    _animation = Tween(
      begin: 0.0,
      end: 1.0,
    ).animate(_controller);
    super.initState();
  }

  @override
  void dispose() {
    // Dispose animation controller when the widget is disposed.
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    // Set the animation with automatics reversal
    _controller.repeat(reverse: true);

    return Scaffold(
      appBar: AppBar(
        title: const Center(child: Text('Animate Icon in Flutter')),
      ),
      body: Center(
        // Create the animated icon
        child: AnimatedIcon(
          color: Colors.orange[300],
          size: MediaQuery.of(context).size.width,
          icon: AnimatedIcons.search_ellipsis,
          progress: _animation,
        ),
      ),
    );
  }
}
```
