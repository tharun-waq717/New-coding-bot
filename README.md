# New-coding-bot
New code
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Calculator',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: CalculatorScreen(),
    );
  }
}

class CalculatorScreen extends StatefulWidget {
  @override
  _CalculatorScreenState createState() => _CalculatorScreenState();
}

class _CalculatorScreenState extends State<CalculatorScreen> {
  String input = '';

  // Update input when a button is pressed
  void buttonPressed(String value) {
    setState(() {
      input += value;
    });
  }

  // Calculate the result of the input expression
  void calculateResult() {
    try {
      final result = input.isNotEmpty ? (int.tryParse(input) ?? 0).toString() : '';
      setState(() {
        input = result;
      });
    } catch (e) {
      setState(() {
        input = 'Error';
      });
    }
  }

  // Clear the input
  void clearInput() {
    setState(() {
      input = '';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Calculator')),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: [
          // Display the input
          Padding(
            padding: const EdgeInsets.all(20.0),
            child: Text(input, style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold)),
          ),
          // Calculator buttons
          Expanded(
            child: GridView.builder(
              gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 4,
                childAspectRatio: 1.0,
              ),
              itemCount: 16,
              itemBuilder: (context, index) {
                List<String> buttons = [
                  '7', '8', '9', '/',
                  '4', '5', '6', '*',
                  '1', '2', '3', '-',
                  '0', '.', '=', '+',
                  'C'
                ];

                return ElevatedButton(
                  onPressed: () {
                    if (buttons[index] == 'C') {
                      clearInput();
                    } else if (buttons[index] == '=') {
                      calculateResult();
                    } else {
                      buttonPressed(buttons[index]);
                    }
                  },
                  child: Text(
                    buttons[index],
                    style: TextStyle(fontSize: 24),
                  ),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
