### 1. GO를 통한 출력

### 2. 변수

### 3. 텍스트

 

### 1. GO를 통한 출력

GO를 실행순서

폴더 생성 -> .go 파일 생성및 작성 -> GO 모듈 생성 -> GO 빌드 -> .exe 실행

 

폴더 생성후 .go 파일 작성 한다.
| | |
|---|---|
|cd /경로|1.작성한 경로로 이동한다|
|go mod init 경로/경로|2.GO 모듈을 생성한다.|
|go build|3.GO 빌드|
|./빌드파일이름.exe|4.파일 실행|

-Hello World! 출력하자

package main  //프로그램에 시작점

import "fmt"   //표준 입출력 패키지

// main 시작함수로 특수한 함수
func main(){

     fmt.println("Hello World! ")//세미콜론이 없다!

}
저장 후 위에 build 작업순서 실행

 

2. 변수

GO는 변수선언시 변수 선언 키워드가 있다.

package main  //프로그램에 시작점

import "fmt"   //표준 입출력 패키지

// main 시작함수로 특수한 함수
func main() {
	var a int = 10                 //var 변수 선언 키워드
	var msg string = "Good Night"  // 엥 String이 대문자가 아니다. 클래스가 없어서 그런가?

	a = 20
	msg = "Good Moring"

	fmt.Println(msg, a)
    //Good Moring 20
    
    // 변수 선언 다른형태 :=
    var a int = 3  //기본 형태
    var b int      //초기값 생략시 정의되있는 각 타입에 기본값 Defult = 0
    var c = 4      //타입 생략 int,string 타입이 없어도 값이 int형이면 int로 정의
    d := 5         // := 는 var와 타입을 생략하고 선언  
    
    fmt.Println(a,b,c,d)
    //3 0 4 5
}
GO 언어에 경우 강타입 언어로 int 에 float 등에 다른 타입넣을시 에러 발생

그렇기에 정수를 실수단위로 바꾸려면 타입변환이 필요한다.

package main
import "fmt"

func main() {
	a := 3              // var 생략 3
	var b float64 = 3.5 // 64비트 float
	fmt.Println(a, b)   // 3     3.5

	// int에 경우 컴퓨터 32비트 컴퓨터에서 int32 ,컴퓨터 64비트 컴퓨터에서 int64
	var c int = int(b)  // float64 -> int 형으로 변환 3.5 -> 변환시 소수점 버림
	d := float64(a * c) // int a * c
	fmt.Println(c, d)   // 3     9

	var e int64 = 7   // int64 (-9223372036854775808 ~ 9223372036854775808)
	f := int64(d) * e // int64 = 9 * 7
	fmt.Println(e, f) // 7     63

	var g int = int(b * 3) // float int로 변환시 3.5 * 3 = 10.5 변환시 수소점 제거   = 10
	var h int = int(b) * 3 // float int로 변환시 3.5 변환시 소수점 제거 =3  -> 3 * 3 = 9
	fmt.Println(g, h, f)   // 10 9 63
}
int 선언시 64,32 지정해줘서 선언이 변할것 같다.

소수점 자리등 중요한 값에 규모가 클경우 float,int 값 범위 지정 주의

 

3.텍스트

입출력시 import "fmt" 사용해야 한다.

fmt.println 을 통한 출력 사용법

package main

import "fmt"

func main() {
	var a int64 = 10
	var b int64 = 20
	var f float64 = 32799438743.8297

	fmt.Println("a:", a, "b:", b, "f:", f)        // 출력후 자동 개행
	fmt.Printf("a: %d  b: %d  f: %f \n", a, b, f) // 서식을 통한 출력시 printf 사용

	// 연습도중 특이사항으로 변수를 선언후 사용하지 않으면 알람 및 실행에러가 발생합니다.
}
 

fmt.Scan 을 통한 입력방법

package main
import "fmt"

func main() {
	var a int
	var b int

	n, err := fmt.Scan(&a, &b) 
    	// 포인터 &a, &b 메모리 공간을 가리킨다. 값을 메모리 주소에 넣어라
	// 위에서 int형 선언 넣은값이 int가 아니면 문제 발생
	// Scan 함수는 return 값으로 n은 입력된 갯수 err 는 에러 사항이 있으면 반환한다.
	if err != nil { // nil = null
		fmt.Println(n, err)
		fmt.Println(n, err)
	} else {
		fmt.Println(n, a, b, err)
	}
}
정상 입력시 값 반환 2 1 22 <nil>
