# Animate Opacity in Flutter

```dart
// 1. We will store a value of type "double" for image's opacity
// and switch it value between 0.5 and 1.0 when user taps on image.
// So we extends StatefulWidget here.
class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  // 2. And then we store the opacity value in _opacity,
  // with the value 0.5 so the image is half tranparent.
  double _opacity = 0.5;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Animate Opacity'),
      ),
      // 3. And then we wrap image with gesture so we can detect taps
      // on the image and as a result we can switch the opacity
      // between 0.5 and 1.0.
      body: GestureDetector(
        // 4. When the image is tapped, we take the current value of 
        // _opacity and calculate that minus 1.5, and then return
        // the absolute result.
        onTap: () => setState(() => _opacity = (_opacity - 1.5).abs()),
        // 5. AnimatedOpacity is an animated view that allows us to
        // animate the change in opacity to its child using
        // opacity and duration parameters.
        child: AnimatedOpacity(
          opacity: _opacity,
          duration: const Duration(seconds: 1),
          child: Image.asset('assets/img.jpg'),
        ),
      ),
    );
  }
}
```
