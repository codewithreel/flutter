# Animate Widget Shadow in Flutter

```dart
class ImageTransition extends AnimatedWidget {
  const ImageTransition({
    super.key,
    required this.imageUrl,
    shadowXOffset,
  }) : super(listenable: shadowXOffset);

  final String imageUrl;
  Animation<double> get shadowXOffset => listenable as Animation<double>;

  @override
  Widget build(BuildContext context) {
    return Container(
      clipBehavior: Clip.antiAlias,
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(20),
        boxShadow: [
          BoxShadow(
            blurRadius: 10,
            offset: Offset(shadowXOffset.value, 20),
            color: Colors.black.withAlpha(100),
            spreadRadius: -10,
          )
        ],
      ),
      child: Image.asset(imageUrl),
    );
  }
}

class CustomCurve extends CurveTween {
  CustomCurve() : super(curve: Curves.easeInOutSine);

  @override
  double transform(double t) {
    return (super.transform(t) - 0.5) * 25.0;
  }
}

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen>
    with SingleTickerProviderStateMixin {
  late final AnimationController _controller;
  late final Animation<double> _animation;

  @override
  void initState() {
    _controller = AnimationController(
      vsync: this,
      duration: const Duration(seconds: 1),
    );
    _animation = CustomCurve().animate(_controller);
    super.initState();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    _controller.repeat(reverse: true);

    return Scaffold(
      body: Padding(
        padding: const EdgeInsets.all(8),
        child: Center(
          child: ImageTransition(
            imageUrl: 'assets/img.jpg',
            shadowXOffset: _animation,
          ),
        ),
      ),
    );
  }
}
```
