import 'package:flutter/material.dart';

void main() => runApp(BMICalculatorApp());

class BMICalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: BMICalculator());
  }
}

class BMICalculator extends StatefulWidget {
  @override
  _BMICalculatorState createState() => _BMICalculatorState();
}

class _BMICalculatorState extends State<BMICalculator> {
  double height = 160;
  double weight = 60;
  double? _bmi;

  void _calculateBMI() {
    final h = height / 100;
    setState(() {
      _bmi = weight / (h * h);
    });
  }

  String _bmiCategory(double bmi) {
    if (bmi < 18.5) return "Underweight";
    if (bmi < 24.9) return "Normal";
    if (bmi < 29.9) return "Overweight";
    return "Obese";
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('BMI Calculator')),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Adjust your height and weight to calculate your BMI.',
              style: TextStyle(fontSize: 16),
            ),
            SizedBox(height: 20),
            Text('Height: ${height.toStringAsFixed(1)} cm',
                style: TextStyle(fontSize: 18)),
            Slider(
              value: height,
              min: 100,
              max: 220,
              onChanged: (val) => setState(() => height = val),
            ),
            SizedBox(height: 10),
            Text('Weight: ${weight.toStringAsFixed(1)} kg',
                style: TextStyle(fontSize: 18)),
            Slider(
              value: weight,
              min: 30,
              max: 150,
              onChanged: (val) => setState(() => weight = val),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _calculateBMI,
              child: Text('Calculate BMI'),
            ),
            SizedBox(height: 20),
            if (_bmi != null) ...[
              Text(
                'Your BMI is ${_bmi!.toStringAsFixed(1)}',
                style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
              ),
              Text(
                'Category: ${_bmiCategory(_bmi!)}',
                style: TextStyle(fontSize: 18),
              ),
            ]
          ],
        ),
      ),
    );
  }
}
