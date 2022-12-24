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
2. App 사용가능한 박스 위젯

2-1 글자 사용 예제
``` dart
       const Text(
            'FLUTTER',
            style: TextStyle(
              fontSize: 20,
              fontWeight: FontWeight.w700,
              color: Colors.red,
            ),
          ),
          ## 아이콘
         const Icon(Icons.star)
         ##이미지 불러오기 불러오기번에 세팅해야한다
         ## pubspec.yaml
         ## flutter:
         ##   assets:
         ##     - assets/
         ## 경로를 추가해줘야 사용할수 있다
         Image.asset("assets/Lenna.png")
         ## 가운데 정렬
         Center()
```

2-5 여러개 사용시 

 Row(
            ## 가운데 사이간격 정렬
            mainAxisAlignment: MainAxisAlignment.center,
            children :const [
              Icon(Icons.star),
              Icon(Icons.star),
              Text("test"),
            ]
          )

 Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children :const [
              Icon(Icons.star),
              Icon(Icons.star),
              Text("test"),
            ]
        )


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
--------------------------------






