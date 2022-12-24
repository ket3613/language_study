flutter 만들기

-----
1. 시작 
1-1 lib 경로에 main.dart 파일이 시작 파일이다.
1-2 기존 코드정리 및 기본코드 

``` dart
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    ## MaterialApp  구글 스타일에 앱 구성정보 갖고 있다
    ## CupertinoApp IOS  스타일에 앱구성 정보 갖고 있다
    return MaterialApp();
  }
};
``` 

위젯 정리
-------------------------------
3. App 구분 및 위치

``` dart
  @override
  Widget build(BuildContext context) {
    
    ## google_style_app
    return MaterialApp(
    ## Scaffold 사용시 3단 구분을 사용하기위한 기본함수
      home: Scaffold(
        ##  appBar: 상단바
        appBar: AppBar(),
        
        ##  body: 중단바
        body: body: Container(),
        
        ##  bottomNavigationBar: 하단바
        bottomNavigationBar: BottomAppBar(),
      )
    );
  }
``` 







