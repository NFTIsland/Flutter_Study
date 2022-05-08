# Flutter

## Widget
### Widget이란 : 독립적으로 실행되는 작은 프로그램, 그래픽이나 데이터 요소를 처리하는 함수를 가지고 있음
	     ★UI를 만들고 구성하는 모든 기본 단위 요소.(앱화면을 구성하는 모든 요소들을 통들어 위젯) (눈에 보이지 않는 요소들까지 포함)
	      ->플러터에선 모든 것이 위젯으로 시작해서 위젯으로 끝남. 
	     ★모든 위젯들은 클래스로 만들어진 인스턴스.
	     위젯들은 트리 구조로 연결되어짐.
	     ★모든 커스텀 위젯은 클래스 내에 각각 또다른 위젯을 리턴하는 build라는 함수를 가지고 있음. 
		   build는 어떤 위젯을 만들지 정의하는 함수 
		   Widget build(buildContext context){ return 위젯();}
	       ->build에서 실행시킬 위젯을 return함.

### Widget 종류 : 
	1. Stateless Widget : 상태가 정적인 위젯(변하지 않음), 실시간 데이터나 변화를 유발시키는 value값 X(없음)
	2.  Stateful Widget : 계속해서 변화가 있는 위젯
	    만약 커스텀 Stateless Widget을 만들고 싶다면 class 이름 extends StatelessWidget{}으로 만들면 되고 
		커스텀 Stateful Widget을 만들고 싶다면 class 이름 extends Stateful Widget{}으로 만들고 
		위젯의 상태를 계속해서 감시하기 위해서 {} 안에 State createState(){} 를 선언하고 createState의 { } 안에 감시하고자 하는 위젯을 return한다. 
		여기서는 build 함수 X, 또한 감시하고자 하는 위젯은 class 이름 extends State{} 꼴로 만든다.
### Dart에서
   	★모든 위젯들은 클래스 꼴로 구성되어 있고 각각의 인자를 가지고있는데 원하는 인자만 골라서 값을 전달해줄 수 있음.
	위젯에서 인자에게 값을 전해줄 때는 인자이름 : value 식으로 전달해줌 value에 위젯을 전달해 줄 수도 있음.
	ex : MaterialApp(theme : ThemeData()) //Material 위젯의 theme 인자에 ThemeData()라는 위젯 전달.
   	만약 위젯의 인자(속성)이 뭐가 있는지 궁금하다면 ctrl + space를 눌러볼 것.


### Flutter Widget Tree : Widget들은 Tree 구조로 정리될 수 있음
	1. 한 Widget내에 얼마든지 다른 widget들이 포함될 수 있음.
	2. Widget들은 부모 위젯과 자식 위젯으로 구성
	3. Parent widget을 widget container라고 부르기도 함

## 폴더
### 폴더 분류
	1. lib : 우리가 코딩하는 dart가 속해있는 폴더
	2. pubspec.yaml : 메타데이터 관리, 군대에서 물자, 보급 추가되면 보고하듯이 앱내에 데이터들을 추가했다면(ex:이미지, 폰트) pubspec.yaml에 명시해야함. 
	★들여쓰기가 아주 민감하므로 주석처리 되어 있는 것이랑 똑같은 형식으로 적을 것



## Stateful 위젯의 생명주기 10단계
	1. createState() 함수 : Stateful 위젯 함수는 반드시 createState()함수를 호출해야 함, 감시할 State클래스를 return 함
	2. mounted == true : createState()함수가 호출되면 mounted 속성이 true로 변경, -> buildContext 클래스에 접근 가능 -> setState()함수 사용가능 
   						 setState()함수란 상태가 바뀌었을 때 현재 화면에 적용하는 함수.
	3. initState() 함수 : 위젯 초기화 할 때 제일 먼저 호출, 용도 : 데이터 목록을 만들거나, 처음 필요한 데이터 주고받을 때
	4. didChangeDependencies() 함수 : initState랑 쌍으로 호출되는 함수, 위젯이 데이터에 의존하는 위젯이라면 꼭 호출
	5. build()함수 : Widget을 반환, 화면에 렌더링함.
	6. didUpdateWidget()함수 : 위젯이 변경되거나 해서 갱신해야 할 때.(initState는 처음 한번만 호출되므로 이후에 필요)
	7. setState() 함수 : 데이터가 변경되었다는 것 알림, 변경된 데이터로 화면 UI 변경
	8. deactivate()함수 : State 객체 중지
	9.  dispose()함수 : State객체를 영구적으로 삭제
	10. mounted == false : 객체가 소멸되면 false로 변경, 해당 State를 재사용할 수 없음.

## 코딩
	1. import 'package:flutter/material.dart'; : 플러터에서 앱을 꾸미기 위한 기능들이 담긴 material을 추가하는 것. 
   												 이걸 추가하지 않는다면 아무런 재료 없이 무언가를 만들겠다는 것과 같음.

	2. runApp() : flutter의 최상위에 위치한 위젯, 실행시킬 위젯을 인자로 받음. main에서 실행시킴, 이걸 넣지 않으면 app이 실행이 안됨. 

	3. Material App() : import한 flutter/material 라이브러리를 사용할 수 있는 기능을 가진 위젯, material을 import해도 Material App()이 아니면 사용할 수 없음.
	    속성 : 	* title // 앱의 이름을 설정
         		* theme // 테마를 결정, 보통 theme: ThemeData()꼴로 ThemeDate() 위젯을 실행시켜주는 듯 함.
     		    * home // 맨 처음 보여줄 화면을 설정 **home:에 바로 Scaffold 위젯을 전달해서 꾸며도 되지만 
  						  나중에 복잡한 앱을 구성할 때에는 유지보수상 여러개의 파일로 나누어서 실행시키는 것이 유지보수에 유리하기 때문에
						  home에 바로 scaffold를 실행시키는 것보단 위젯들을 만들어서 실행시키는 것이 좋음

	4. Scaffold() : 앱 화면과 기능을 구성하기 위한 페이지를 준비해주는 위젯, 없으면 아무것도 꾸밀 수 없음, 음식 먹기 전에 책상 닦고 세팅하는 것 같은 느낌
 	    속성 : * appbar: AppBar() // 앱 화면의 상단을 꾸미는 인자에 AppBar()라는 위젯 입력, AppBar에는 title 인자와 centerTitle인자와 elevation이 있는데 
	  	  	   					     centerTitle은 titled을 appbar의 중앙으로 위치할 것인지 설정하는 인자, elevation은 나머지 영역에 비해 떠있는 느낌을 조절할 수 있는 인자.
	    	 ★Material app에서 title인자와 Scaffold의 AppBar에서 title 인자의 차이점 : Material app의 title은 앱의 이름이라고 생각하면 되고,
			   AppBar()의 title은 앱 화면 상단에 출력되는 값
	           * body // Scaffold 위젯 내에서 본격적으로 앱 화면을 만드는 시작점.
	           * floatingActionButton // 떠있는 버튼 만드는 것 ex:) floatingActionButton : FloatingActionButton(child : Icon(Icons.add)) -> 더하기 모양의 떠있는 아이콘 생성
	5. Icon() :  아이콘 생성
	6. Center() : 화면의 가로를 기준으로 가운데에 정렬
	7. Column(), Row() : 세로로 혹은 가로로 여러개의 위젯을 넣고 싶을 때 사용, 위젯을 여러개 넣을 수 있기 때문에 하나의 위젯만 넣더라도 항상 child가 아닌 children 인자를 					  사용하며 배열로 선언해서 []안에 여러개를 입력한다.
	    				 ex : Column(children : <Widget>[~~~~])
	    속성 : * mainAxisAlignment : MainAxisAlignment.center // Row()의 경우에는 가로로 중앙, Column의 경우 세로로 중앙
	    	   * crossAxisAlignment : CrossAxisAlignment.start // Row()의 경우에는 세로로 중앙, Column의 경우에는 가로로 중앙 정렬
	8. Padding() : 화면 간격 조절
		속성 : * EdgeInsets // Padding 공간의 상하좌우 간격 조절하게 하는 것.

	9. Text() : 텍스트
		속성 : * style:TextStyle() // TextStyle위젯 내에는 color, letterSpacing, fontSize, fongWeight등 속성이 있고 이를 통해 꾸밀 	수 있다.

	10. SizedBox() : 위젯 사이 공백을 넣고 싶을 때 사용
		속성 : * height
	    	   * width

	11. CircleAvartar()  : 이미지를 원형의 공간에 넣고 싶을 때 사용, backgroundImage: 속성을 이용해서 AssetImage(경로)꼴로 추가해준다.
		속성 : * backgroundImage : AssetImage(경로) // 이미지 추가
    	       * radius // 원 크기 설정

    12.  ElevatedButton() : 네모난 버튼 생성
		속성 : * child: const Text()//버튼 이름
	           * onPressed:(){} // 버튼을 눌렀을 때 실행하는 함수 { } 안에 실행할 코드를 입력, 보통 화면을 변경해야 하기 때문에 setState()가 있음

	13.  TextField() : 텍스트 입력하는 공간 생성 줄로 표시됨
		속성 : * keyboardType // TextInputType.number로 하면 TextField를 눌렀을 때 숫자패드의 키보드가 나옴.
	    	   * controller // 해당 TextField의 값을 어떤 변수에 넣을지.

	14.  DropdownButton() : 누르면 목록이 나오는 버튼
		속성 : * item // 목록을 입력 -- DropdownMenuItem<String> 형태의 값을 리스트로 받음
						 ex:) List<DropdownMenuItem<String>> _dropDownMenuItems, _dropDownMenuItems.add(value : ~, child : Text(~))
     	       * onChanged // 아이템이 바뀔 때 처리하는 이벤트
	           * value : 버튼에 출력할 데이터(이름)

