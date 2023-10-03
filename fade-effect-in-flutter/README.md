# Fade Effect in Flutter

```dart
class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  // Define _isContainerVisible to store boolean for
  // indicating if Container is visible or not.
  bool _isContainerVisible = true;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(child: Text('Fade Effect in Flutter')),
      ),
      body: Center(
        child: Column(
          children: [
            // AnimatedOpacity is used to enable fade animations.
            AnimatedOpacity(
              // When opacity is 1.0, Container will be visible.
              // And when opacity is 0.0, Container will be invisible.
              opacity: _isContainerVisible ? 1.0 : 0.0,
              duration: const Duration(seconds: 1),
              child: Container(
                width: 100,
                height: 100,
                color: Colors.blue,
              ),
            ),
            TextButton(
              // When the button is pressed we flip the boolean for visible or invisible.
              onPressed: () => setState(() => _isContainerVisible = !_isContainerVisible),
              child: Text('Press'),
            ),
          ],
        ),
      ),
    );
  }
}
```
