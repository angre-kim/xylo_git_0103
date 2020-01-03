# xylo_git_0103

A new Flutter application.

# 섹션9-xylophone

## 70강-How to Play Sound Across Platforms

- Stless로 MaterialApp 만들고 home에Sca body에 safearea child에 Center 위젯 만들기 flatButton 만들기

        import 'package:flutter/material.dart';
        import 'package:audioplayers/audio_cache.dart';
        
        void main() => runApp(XylophoneApp());
        
        class XylophoneApp extends StatelessWidget {
          @override
          Widget build(BuildContext context) {
            return MaterialApp(
              home: Scaffold(
                body: SafeArea(
                  child: Center(
                      child: FlatButton(

- onPressed

        Widget build(BuildContext context) {
            return MaterialApp(
              home: Scaffold(
                body: SafeArea(
                  child: Center(
                      child: FlatButton(
                          onPressed: () {
                            final player = AudioCache();
                            player.play('asset/note1.wav');
                          },
                          child: Text('click'))),
                ),
              ),
            );

## 71강

- Center를 column 위젯으로 변경, Flatbutton 컬러 주기, 7개 복사하기,

        body: SafeArea(
                    child: Column(
                  children: <Widget>[
        
                    FlatButton(
                      color: Colors.red,
                      onPressed: () {
                                 final player = AudioCache();
                        player.play('asset/note1.wav');
        
        
                      },
                    ),
                  ],
                )),

- playSound 펑션 만들기

        class XylophoneApp extends StatelessWidget {
          
          void playSound() {
            
            final player = AudioCache();
            player.play('asset/note1.wav');
            
          }
        
        @override
          Widget build(BuildContext context) {
            return MaterialApp(
              home: Scaffold(
                body: SafeArea(
                    child: Column(
                  children: <Widget>[
        
                    FlatButton(
                      color: Colors.red,
                      onPressed: () {
                        playSound();
                      },
                    ),

- playSound 초기값 만들기 playSound(int soundNumber)

        void playSound(int soundNumber) {
            
            final player = AudioCache();
            player.play('asset/note$soundNumber.wav');
        
        
        //중간 생략
        
        FlatButton(
                      color: Colors.red,
                      onPressed: () {
                        playSound(1);
                      },
                    ),

72강-fucntion 설명

    void main(){
    
    greet('jack');
    }
    
    void greet(String persontogreet){
    print('hello $persontogreet');
    }

    void main(){
    
    greet('how do you do?,'jack');
    }
    
    void greet(String greeting, String persontogreet){
    print('$greeting $persontogreet');
    }

    void main(){
    
    greet(greeting:'how do you do?',persontogreet:'jack');
    }
    
    
    void greet(String greeting, String persontogreet){
    print('$greeting $persontogreet');
    }
    //에러 남

    void main(){
    
    greet(greeting:'how do you do?',persontogreet:'jack');
    }
    
    
    void greet({String greeting, String persontogreet}){
    print('$greeting $persontogreet');
    }
    //{}삽입하면 정상 작동

    void getmilk (int bottles){
      double cost = bottles * 1.5;
    }
    
    getmilk(2);
    
    //위 아래 모두 같은 결과이지만 아래의 코드가 더 보기 쉽다. 그렇게 하려면 {}를 사용해라
    
    
    void getmilk ({int numbottles}){
      double cost = bottles * 1.5;
      
    }
    
    getmilk(numbottles: 2);

## 73강

- Scaffold backgroundcolor를 black으로 변경

        

- Expanded widget를 사용하여 7개 Flatbutton를 모두 변경

        child: Column(
                  children: <Widget>[
                    //wrap with new widget
                      Expanded(
                      child: FlatButton(
                        color: Colors.red,
                        onPressed: () {
                          playSound(1);
                        },
                      ),
                    ),

- column 에서 crossAxixAlinement: crossAxixAlinemen.stretch로 변경
- Expanded 부분을 list로 만들기 위해 buildKey function 만들기

        void buildKey(){
            Expanded(
              child: FlatButton(
                color: Colors.red,
                onPressed: () {
                  playSound(1);
                },
              ),
            );
        
        //생략
        
        body: SafeArea(
                    child: Column(crossAxisAlignment:CrossAxisAlignment.stretch,
                  children: <Widget>[
                    buildKey();
                    buildKey(),
                    buildKey(),
                    buildKey(),
                    buildKey(),
                    buildKey(),
                    buildKey(),
        // void 에러 발생
        

## 74강, 75강 return 값 있는 function설명

## 76강

- void buildKey function 에러 수정하기

        Expanded buildKey(){       //output data type이 Expanded
           return
             Expanded(
              child: FlatButton(
                color: Colors.red,
                onPressed: () {
                  playSound(1);
                },
              ),
            );
        
        //생략
        
        body: SafeArea(
                    child: Column(crossAxisAlignment:CrossAxisAlignment.stretch,
                  children: <Widget>[
                    buildKey();
                    buildKey(),
                    buildKey(),

- buildKey()을 다르게 주기

        Expanded buildKey(){       //output data type이 Expanded
           return
             Expanded(
              child: FlatButton(
                color: Colors.red,
                onPressed: () {
                  playSound(1);
                },
              ),
            );
        
        //생략
        
        body: SafeArea(
                    child: Column(crossAxisAlignment:CrossAxisAlignment.stretch,
                  children: <Widget>[
                    buildKey(color:Color.red, soundNumber: 1),//에러 발생
                    buildKey(),

- 생성자 주기로 에러 수정

        Expanded buildKey({Color color, int soundNumber}){
            return
              Expanded(
        //생략
        
        
                  children: <Widget>[
                    buildKey(color:Colors.red, soundNumber: 1),
        
        //생력. 다시 이 부분 수정
        
        
        return
              Expanded(
              child: FlatButton(
                color: **color,**
                onPressed: () {
                  playSound(soundNumber);
