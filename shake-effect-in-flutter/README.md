# Shake Effect in Flutter

```dart
const animationWidth = 10.0;

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

// SingleTickerProviderStateMixin is a mixin that
// provides a single-tick animation controller.
class _HomeScreenState extends State<HomeScreen>
    with SingleTickerProviderStateMixin {
  late final TextEditingController _textController;
  final defaultHintText = 'Enter your email here';
  // Define _hintText that store hint text for the text field.
  // When the user forgets to enter a value in the text field
  // and taps on the Login button, we change hint.
  var _hintText = '';

  // There are two key components, AnimationController that controls
  // the duration of the animation and an animation object of type
  // Animation<T> that specifies the animation to be
  // applied.
  // In the case we adjust the offset of the text field so we 
  // need an Animation<num>.
  late final AnimationController _animationController;
  late final Animation<num> _offsetAnimation;

  @override
  void initState() {
    // Setup the text editing controller.
    _textController = TextEditingController();
    _hintText = defaultHintText;

    // Setup the animation controller.
    _animationController = AnimationController(
      duration: const Duration(milliseconds: 370),
      vsync: this,
    );
    // The actual Tween animation that shake the box horizontally
    _offsetAnimation = Tween(
      begin: 0,
      end: animationWidth,
    ).chain(CurveTween(curve: Curves.elasticIn))
        .animate(_animationController)
            ..addStatusListener(
              (status) {
                if (status == AnimationStatus.completed) {
                  _animationController.reverse();
                }
              },
            );
    super.initState();
  }

  @override
  void dispose() {
    _textController.dispose();
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(child: Text('Shake Effect in Flutter')),
      ),
      body: Column(
        children: [
          AnimatedBuilder(
            animation: _offsetAnimation,
            builder: (context, child) {
              return Container(
                margin: const EdgeInsets.symmetric(horizontal: animationWidth),
                padding: EdgeInsets.only(
                  left: _offsetAnimation.value + animationWidth,
                  right: animationWidth - _offsetAnimation.value,
                ),
                child: TextField(
                  controller: _textController,
                  keyboardType: TextInputType.emailAddress,
                  decoration: InputDecoration(hintText: _hintText),
                ),
              );
            },
          ),
          TextButton(
            onPressed: () async {
              if (_textController.text.isEmpty) {
                setState(() {
                  _hintText = 'Forgot to enter your email';
                  _animationController.forward(from: 0);
                });
                await Future<void>.delayed(const Duration(seconds: 3));
                setState(() => _hintText = defaultHintText);
              }
            },
            child: const Text('Login'),
          ),
        ],
      ),
    );
  }
}
```
