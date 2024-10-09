- 👋 Hi, I’m @mariana-oliveira07
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
mariana-oliveira07/mariana-oliveira07 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Fase da Vida',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: FaseDaVidaScreen(),
    );
  }
}

class FaseDaVidaScreen extends StatefulWidget {
  @override
  _FaseDaVidaScreenState createState() => _FaseDaVidaScreenState();
}

class _FaseDaVidaScreenState extends State<FaseDaVidaScreen> {
  final TextEditingController _controller = TextEditingController();
  String _resultado = '';
  String _erro = '';

  void determinarFaseDaVida(int idade) {
    setState(() {
      if (idade < 3) {
        _resultado = 'Infância';
      } else if (idade >= 3 && idade <= 12) {
        _resultado = 'Pré-adolescência';
      } else if (idade >= 13 && idade <= 19) {
        _resultado = 'Adolescência';
      } else if (idade >= 20 && idade <= 35) {
        _resultado = 'Juventude';
      } else if (idade >= 36 && idade <= 55) {
        _resultado = 'Meia-idade';
      } else if (idade >= 56) {
        _resultado = 'Terceira idade';
      }
    });
  }

  void _onPress() {
    setState(() {
      _erro = '';  // Limpa o erro antes de validar
      String input = _controller.text.trim();  // Remove espaços em branco
      if (input.isEmpty) {
        _erro = 'Por favor, insira sua idade';
        _resultado = '';
      } else if (!RegExp(r'^[0-9]+$').hasMatch(input)) {
        _erro = 'Apenas números são permitidos';
        _resultado = '';
      } else {
        int idade = int.parse(input);  // Converte a string para inteiro
        if (idade > 116) {
          _erro = 'A idade máxima permitida é 116 anos';
          _resultado = '';
        } else {
          determinarFaseDaVida(idade);
        }
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Determinar Fase da Vida'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: _controller,
              decoration: InputDecoration(
                labelText: 'Digite sua idade',
                errorText: _erro.isNotEmpty ? _erro : null,
              ),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _onPress,
              child: Text('Determinar Fase da Vida'),
            ),
            SizedBox(height: 20),
            Text(
              _resultado,
              style: TextStyle(fontSize: 24),
              textAlign: TextAlign.center,
            ),
          ],
        ),
      ),
    );
  }
}
