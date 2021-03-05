# myfirst-app
import 'package:flutter/material.dart';
import 'package:my_first_app01/quize.dart';
import 'result.dart';

void main() => runApp(NewApp());

class NewApp extends StatefulWidget {
  @override
  _NewAppState createState() => _NewAppState();
}

Color wthem = Colors.white;
Color bthem = Colors.black;
bool switchbool = false;

class _NewAppState extends State<NewApp> {
  int _qusetionindex = 0;
  int _totalscore = 0;
  var num0 = 0, num1 = 0, num2 = 0;
  void _restartApp() {
    setState(() {
      _qusetionindex = 0;
      _totalscore = 0;
      num0 = 0;
      num1 = 0;
      num2 = 0;
    });
  }

  void _ansqusetionindex(score) {
    if (_qusetionindex == 0)
      num0 = score;
    else if (_qusetionindex == 1)
      num1 = score;
    else if (_qusetionindex == 2) num2 = score;
    setState(() {
      _totalscore += score;
      _qusetionindex += 1;
    });
  }

  List<Map<String, Object>> _qusetionS = [
    {
      'qusetiontext': 'ماهو نوع حيوانك المفضل ',
      'answerstext': [
        {'text': 'القطة', 'score': 40},
        {'text': 'العصافير', 'score': 30},
        {'text': 'الحصان', 'score': 20},
        {'text': 'الكلب', 'score': 10}
      ]
    },
    {
      'qusetiontext': 'ماهى سمات حيوانك المفضل',
      'answerstext': [
        {'text': 'هادئ', 'score': 30},
        {'text': 'مرح', 'score': 40},
        {'text': 'سريع', 'score': 20},
        {'text': 'غاضب', 'score': 10}
      ]
    },
    {
      'qusetiontext': 'ماهو مكانك المفضل لك مع حيوانك ',
      'answerstext': [
        {'text': 'الحديقة', 'score': 40},
        {'text': 'البيت', 'score': 30},
        {'text': 'متنزهات عامة', 'score': 20},
        {'text': 'الطريق السريع', 'score': 10}
      ]
    }
  ];
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          actions: <Widget>[
            Switch(
                activeColor: Colors.white,
                activeTrackColor: Colors.black,
                inactiveThumbColor: bthem,
                value: switchbool,
                onChanged: (value) {
                  setState(() {
                    switchbool = value;
                    if (switchbool == true) {
                      bthem = Colors.white;
                      wthem = Colors.black;
                    }
                    if (switchbool == false) {
                      bthem = Colors.black;
                      wthem = Colors.white;
                    }
                  });
                }),
          ],
          title: Text(
            ' تعرف على شخصيتك سؤال وجواب',
            textAlign: TextAlign.left,
            style: TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.bold,
                color: Colors.green[100]),
          ),
          backgroundColor: Colors.blue[800],
        ),
        body: Container(
          color: wthem,
          child: _qusetionindex < _qusetionS.length
              ? Quize(_qusetionS, _qusetionindex, _ansqusetionindex)
              : Result(_restartApp, _totalscore),
        ),
        floatingActionButton: FloatingActionButton(
          child: Icon(
            Icons.arrow_back,
            color: wthem,
            size: 35,
          ),
          onPressed: () {
            if (_qusetionindex == 1)
              _totalscore -= num0;
            else if (_qusetionindex == 2)
              _totalscore -= num1;
            else if (_qusetionindex == 3) _totalscore -= num2;
            setState(() {
              if (_qusetionindex > 0) {
                _qusetionindex -= 1;
              }
            });
          },
        ),
      ),
    );
  }
}
