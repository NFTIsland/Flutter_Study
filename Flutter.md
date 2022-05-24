
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

2. Stateful Widget : 계속해서 변화가 있는 위젯
만약 커스텀 Stateless Widget을 만들고 싶다면 class 이름 extends StatelessWidget{}으로 만들면 되고,
커스텀 Stateful Widget을 만들고 싶다면 class 이름 extends Stateful Widget{}으로 만들고 위젯의 상태를 계속해서 감시하기 위해서 {} 안에 State createState(){} 를 선언하고 createState의 { } 안에 감시하고자 하는 위젯을 return한다.
**여기서는 build 함수 X, 또한 감시하고자 하는 위젯은 class 이름 extends State{} 꼴로 만든다.**

### Dart에서

★모든 위젯들은 클래스 꼴로 구성되어 있고 각각의 인자를 가지고있는데 원하는 인자만 골라서 값을 전달해줄 수 있음.
**꼭 전달해야 하는 값이 있다면 클래스를 만들 때 생성자에서 인자 앞에 required를 붙일 것.**

위젯에서 인자에게 값을 전해줄 때는 인자이름 : value 식으로 전달해줌 value에 위젯을 전달해 줄 수도 있음.

ex : 

    MaterialApp(theme : ThemeData()) // Material 위젯의 theme 인자에 ThemeData()라는 위젯 전달.

만약 위젯의 인자(속성)이 뭐가 있는지 궁금하다면 ctrl + space를 눌러볼 것.

#### List
Dart에도 다른 언어들과 마찬가지로 List가 있음. 생성방법은 자바와 유사하고 처음에 리스트를 생성 시 특별히 값을 넣어서 초기화 하지 않는다면 비어있으므로 empty() 메소드 호출, 메소드 안에 growable 속성에 true 값을 넣어서 List가 가변적으로 확장될 수 있게 설정함.
ex:

    List<String>list.empty(growable:true); // String형식의 확장될 수 있는 비어있는 리스트 호출

#### Call back
Flutter는 코드를 작성하다 보면 특정 이벤트가 발생했을 때 실행하는 함수들이 있다. 이를 콜백 함수라 하고 그렇다 보니 위젯에서 인자로 변수가 아닌 함수를 받는다. 이때 함수는 꼭 이미 만들어진 것을 넘길 필요는 없고 인자와 함수 실행 구문을 넘겨줘도 된다
ex : `itemBuilder : (인자들){실행할 구문}`

### NULLSAFETY

FLUTTER에 추가된 아주 중요한 것이라는 얘기가 많아 가볍게 정리하고자 함.

  

변수를 선언할 때마다 꼭 초기화를 해줘야 함.

그런데 변수를 선언할 때 **자료형 뒤에 ?가 붙으면 초기화를 해주지 않아도 되고** 해당 변수가 NULL값이 들어있을 수도 있다는 것을 알려줌, **NULL값으로 초기화가 가능함.**

반대로 ?가 안붙었으면 값에 NULL을 넣으면 에러가 남

만약 변수를 사용할 때 **NULL이 절대 아니라는 것을 알려주고 싶다면 변수 이름 뒤에 !를 붙혀서 표시함.**

이를 통해서 NULL 값을 잘못 접근해서 프로그램이 에러가 나는 상황을 줄일 수 있음.

  
  
  

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
 `State createState() => 감시할 위젯;`

2. `mounted == true` : createState()함수가 호출되면 mounted 속성이 true로 변경, -> buildContext 클래스에 접근 가능 -> setState()함수 사용가능

	setState()함수란 상태가 바뀌었을 때 현재 화면에 적용하는 함수.

3. initState() 함수 : 위젯 초기화 할 때 제일 먼저 호출, 
용도 : 데이터 목록을 만들거나, 처음 필요한 데이터 주고받을 때
`void initState(){};`

4. didChangeDependencies() 함수 : initState랑 쌍으로 호출되는 함수, 위젯이 데이터에 의존하는 위젯이라면 꼭 호출	

5. build()함수 : Widget을 반환, 화면에 렌더링함.
 `Widget build(BuildContext context){ }`

6. didUpdateWidget()함수 : 위젯이 변경되거나 해서 갱신해야 할 때.(initState는 처음 한번만 호출되므로 이후에 필요)
 `void didUpdateWidget(Widget oldWidget){}`

7. setState() 함수 : 데이터가 변경되었다는 것 알림, 변경된 데이터로 화면 UI 변경
`setState(()=>변경시킬 것);`

8. deactivate()함수 : State 객체 중지

9. dispose()함수 : State객체를 영구적으로 삭제 
 `void dispose(){}`

11. mounted == false : 객체가 소멸되면 false로 변경, 해당 State를 재사용할 수 없음.

  

## 코딩

1. `import 'package:flutter/material.dart';` : 플러터에서 앱을 꾸미기 위한 기능들이 담긴 material을 추가하는 것.

	이걸 추가하지 않는다면 아무런 재료 없이 무언가를 만들겠다는 것과 같음.
	
2. `runApp()` : flutter의 최상위에 위치한 위젯, 실행시킬 위젯을 인자로 받음. main에서 실행시킴, 이걸 넣지 않으면 app이 실행이 안됨.

  

3. `Material App()` : import한 flutter/material 라이브러리를 사용할 수 있는 기능을 가진 위젯, material을 import해도 Material App()이 아니면 사용할 수 없음. 실행시키는 main에서 한번만 실행

	속성 : 
	* title // 앱의 이름을 설정
	* theme // 테마를 결정, 보통 theme: ThemeData()꼴로 ThemeDate() 위젯을 실행시켜주는 듯 함.

	* home // 맨 처음 보여줄 화면을 설정 home:에 바로 Scaffold 위젯을 전달해서 꾸며도 되지만
나중에 복잡한 앱을 구성할 때에는 유지보수상 여러개의 파일로 나누어서 실행시키는 것이 유지보수에 유리하기 때문에
**home에 바로 scaffold를 실행시키는 것보단 위젯들을 만들어서 실행시키는 것이 좋음**

  

4. `Scaffold()` : 앱 화면과 기능을 구성하기 위한 빈 페이지를 준비해주는 위젯, 없으면 아무것도 꾸밀 수 없음, 음식 먹기 전에 책상 닦고 세팅하는 것 같은 느낌 페이지 수만큼 파일 별로 Scaffold 존재

	속성 : 
	* appbar: AppBar() // 앱 화면의 상단을 꾸미는 인자에 AppBar()라는 위젯 입력, AppBar에는 title 인자와 centerTitle인자와 elevation이 있는데 title 인자는 AppBar 제목 설정하는 인자, centerTitle은 titled을 appbar의 중앙으로 위치할 것인지 설정하는 인자, elevation은 나머지 영역에 비해 떠있는 느낌을 조절할 수 있는 인자.
		★**Material app에서 title인자와 Scaffold의 AppBar에서 title 인자의 차이점**
**Material app의 title은 앱의 이름**이라고 생각하면 되고,
**AppBar()의 title은 앱 화면 상단**에 출력되는 값

	* body // Scaffold 위젯 내에서 본격적으로 앱 화면을 만드는 시작점.

	* floatingActionButton // 떠있는 버튼 만드는 것 
		* ex:) `floatingActionButton : FloatingActionButton(child : Icon(Icons.add)) // 더하기 모양의 떠있는 아이콘 생성`
	* `bottomNavigationBar : TabBar(tabs:\<Tab>\[Tab(), Tab()], controller : 컨트롤러 변수)` // 카카오톡처럼 아래에 탭바를 만들어준다. Tab()안에 icon을 추가하면 탭바에 아이콘이 나타난다.

5. `Icon()` : 아이콘 생성

6. `Center()` : 화면의 가로를 기준으로 가운데에 정렬

7. `Column(), Row()` : 세로로 혹은 가로로 여러개의 위젯을 넣고 싶을 때 사용, 위젯을 여러개 넣을 수 있기 때문에 하나의 위젯만 넣더라도 항상 child가 아닌 children 인자를 사용하며 배열로 선언해서 []안에 여러개를 입력한다.
ex : `Column(children : <Widget>[~~~~])`

	속성 : 	
	* mainAxisAlignment : MainAxisAlignment.center // Row()의 경우에는 가로로 중앙, Column의 경우 세로로 중앙
	* crossAxisAlignment : CrossAxisAlignment.start // Row()의 경우에는 세로로 중앙, Column의 경우에는 가로로 중앙 정렬

8. `Padding()` : 화면 간격 조절

	속성 : 
	* `padding : EdgeInsets` // Padding 공간의 상하좌우 간격 조절하게 하는 것.

  

9. `Text()` : 텍스트

	속성 : 
	* style:TextStyle() // TextStyle위젯 내에는 color, letterSpacing, fontSize, fongWeight등 속성이 있고 이를 통해 꾸밀 수 있다.

  

10. `SizedBox()` : 위젯 사이 공백을 넣고 싶을 때 사용

	속성 : 
	* height

	* width

  

11. `CircleAvartar()` : 이미지를 원형의 공간에 넣고 싶을 때 사용, backgroundImage: 속성을 이용해서 AssetImage(경로)꼴로 추가해준다.

속성 : 
* backgroundImage : AssetImage(경로) // 이미지 추가

* radius // 원 크기 설정

  

12. `ElevatedButton()` : 네모난 버튼 생성

	속성 : 
	* child: const Text()//버튼 이름

	* onPressed:(){} // 버튼을 눌렀을 때 실행하는 함수 { } 안에 실행할 코드를 입력, 보통 화면을 변경해야 하기 때문에 setState()가 있음

  

13. `TextField()` : 텍스트 입력하는 공간 생성 줄로 표시됨

	속성 : 
	* keyboardType // TextInputType.number로 하면 TextField를 눌렀을 때 숫자패드의 키보드가 나옴.

	* controller // 해당 TextField의 값을 어떤 변수에 넣을지.
	* InputDecoration // 데코관련 설정 가능
			* icon //TextField 왼쪽에 아이콘 추가 가능(텍스트도 가능)
			* border //선관련 옵션
	* obscureText // 비밀번호 입력할 때 안보이게 하는 것

  

14. `DropdownButton()` : 누르면 목록이 나오는 버튼

	속성 : 
	* item // 목록을 입력 -- DropdownMenuItem<String> 형태의 값을 리스트로 받음

ex:) `List<DropdownMenuItem<String>> _dropDownMenuItems, _dropDownMenuItems.add(value : ~, child : Text(~))`

	* onChanged // 아이템이 바뀔 때 처리하는 이벤트

	* value // 버튼에 출력할 데이터(이름)

15. `TabBarView()` : 탭별 화면, 컨텐츠를 보여주는 위젯

	속성 : 
	* controller // TabController 형식의 변수를 통해 탭을 제어함

	* `children : <Widget>[]`  탭별로 표시할 위젯들을 순서대로 []안에 넣음

16. `TabBar()` : 탭바 메뉴를 보여주는 위젯

	속성 :
	 * controller // 탭을 제어함

	* `tabs : <Tab>[]`  []안에 Tab() 위젯으로 메뉴들을 넣음 아이콘을 넣을거면 Tab(icon : Icon())

17. `Tab()` : 메뉴 만드는 위젯 child 사용 불가하고 icons이나 Text 사용

18. `Image.asset(경로)` : 이미지 불러옴

	속성(**경로는 필수**) :
	* height
	* width
	* fit // 비율 설정
	
19. `ListView.builder()` : 리스트 만듦

	속성 :
	* `itemBuilder : (context, position){}`  BuildContext와 int를 받아서 트리 위치와 아이템의 순번 반환받는 콜백 함수 필요.
20. `Card()` : 리스트뷰의 아이템을 만드는 함수 여러개의 데이터를 하나의 Node로 만들 때는 child로 Row()나 Column을 추가해서 만듦.
21. `GestureDetector()` : 터치, 끌기 같은 손가락 제스쳐의 변화등을 감지하는 위젯
	속성
	* onTap:(){} // 한번 터치했을 때 실행 시 실행시킬 콜백 함수를 입력받음
22. `AlertDialog()` :  알림창을 띄울 AlertDialog 변수에 무슨 내용을 담을지 설정하는 함수
	속성 :
	 * content // 내용을 입력받음
23. `ShowDialog()` : 알림을 띄우는 함수
	속성 :
	* builder : BuildContext 형식의 변수를 받음, 이 변수에 AlertDialog 내용을 전달함.
	* context : 출력할 BuildContext 값을 받음
24. Radio() : 라디오 버튼을 생성함.(같은 그룹 중 하나만 선택 가능)
	* value : 인덱스
	* groupValue : 그룹화
	* onChanged : 선택됐을 때 호출할 함수 받음(콜백)
25. SingleChildScrollView() : 스크롤 할 수 있게 함  Row()를 썼거나 Column을 썼을 때 즉 List로 만들지 않았을 때 스크롤 할 수 있도록  하는 위젯

26. `FocusScope.of(context).unfocus()` // 키보드가 튀어나왔을 때 빈 곳을 클릭하면 사라지게 함.
## 탭바

한 화면에 모두를 표현하기 힘들 때에는 페이스북, 카카오톡처럼 각 화면들을 연결한 탭바를 사용한다.
필요한 것 :
* TabController
* TabBarView() 위젯
* 실행시킬 컨텐츠(위젯)들
* TabBar() 위젯
* Tab()위젯

기본적으로 탭바를 컨트롤하기 위한 변수가 필요한데 이는 `TabController? 이름;` 으로 선언한다.

만약 탭이 이동할 때 어떤 동작을 추가하고 싶다면 TabController의 addListener((){}) 함수를 사용하자.

TabController 변수는 컨트롤할 탭바의 수, 탭이 이동하면 호출되는 함수를 설정해주어야 하는데 생명주기상 initState(){} 함수에서

`변수 = TabController(length : n, vsync : this);`로 설정하면 n개의 탭바를 관리하는 TabController가 된다.

또한 탭바는 애니메이션을 활용하기에 생명주기상 dispose(){} 함수에서 `변수!.dispose();`를 해주어 메모리 누수를 막아야 한다.

  

Scaffold에서 각 탭 별로 컨텐츠를 실행시켜야 할텐데 Scaffold의 body 속성에서 TabBarView() 위젯을 실행시키는데

`TabBarView(children : <Widget>[위젯들, 위젯들], controller : TabController 변수)` 꼴로 설정 위젯에는 실행시킬 컨텐츠들을 넣는다.

  

bottomNavigationBar 속성에 `TabBar(tabs : <Tab>[])`에서 [] 안에 `Tab()`를 통해서 탭에 표시할 것을 정할 수 있는데,

`Tab(icon : Icon(Icon.looks_one), color : Colors.blue)`를 하면 첫번째 탭에 1이라고 표시된 파란색의 아이콘이 생성된다.

  

-> TabBar()는 탭바 메뉴들을 출력해주는 위젯, 메뉴들은 Tab()을 통해서 생성, 탭바 메뉴별로 실행시킬 컨텐츠,화면은 TabBarView로 생성

이때 TabBar, TabBarView 모두 controller 속성에 TabController 변수를 넣어서 TabController 변수로 제어하며,

TabController 변수는 initState()를 통한 초기화와 dispose()를 통한 종료 필요

_bottomNavigationBar는 아래에 탭바를 생성해주는 역할정도이고 사실 이런 탭바 없이도 화면을 좌우로 스와이프해서 다른 탭으로 넘어갈 수 있음._

### 정리
1. TabController 변수로 Tab을 통제하게 하고, 
2. TabBarView()안에 위젯 형식으로 표시할 컨텐츠들을 다 넣고, 
3. 이 탭들을 육안으로 통제할 Bar를 만들고 싶다면 TabBar위젯 안에 tabs 속성에 Tab()위젯들 추가

## 리스트뷰

    ListView.builder(itemBuilder: (context, position){ return 함수();})

리스트를 통해서 리스트뷰를 만드는 위젯 중에 ListView.builder()위젯이 있음
이 builder()함수는 itemBuilder 속성이 꼭 필요한데,
itemBuilder는 위젯 트리에서 위젯의 위치와 아이템의 순번을 BuildContext와 int 자료형으로 각각 넘겨주며 콜백 함수를 인자로 받음.

Card()함수로 자료구조 중에 List의 Node처럼  ()안에 있는 데이터를 바탕으로 리스트 안에 나열할 Node들을 만듦. 여러개의 자료를 하나의  Node로 만들 때는 `child:`에 Row()나 Column()을 이용해서 만듦.

따라서 itemBuilder를 통해 받은 position 값으로 List의 인덱스마다 각각의 데이터 들을 묶어서 하나의 카드로 만들어서 ListView.builder()가 리스트 형식으로 보여줌.

ListView.builder함수에는 itemCount 속성이 있어서 스크롤 할 수 있는 크기를 제한할 수 있다. 보통 가져온 리스트의 길이로 설정하게 됨.

만약 리스트에서  목록에 있는 것을 터치했을 때 알림창을 띄우고 싶다면 itemBuilder에  터치, 끌기 같은 손가락 제스쳐의 변화등을 감지하는 GestureDetector()를 return 시키고 Card는 GestureDetector의 child로 넣는다.

그리고 GestureDetector에 onTap이라는 인자를 넣는데 onTap은 한번 터치됐을 때 실행되며, 콜백 함수를 인자로 받는다. 이 콜백 함수에 작동하길 원하는 코드를 작성하면 되는데
알람을 띄우고 싶다면 AlertDialog 변수를 생성해서
AlertDialog인자로 content에 text나 띄우고 싶은걸 넣어둔 뒤 showDialog()함수에 builder 인자에 AlertDialog를 리턴받는  BuildContext 형식의 변수를 넘기고 content에 받은 BuildContext 변수를 넣어준다.

## 정렬 : 
mainAxisAlignment : 속성으로 MainAxisAlignment.~를 받는데 기준은 해당 축을 기준으로 함. Row내에서 정렬 시 좌우 공간을 기준으로, Column내에서 정렬 시 위 아래 공간을 기준으로
crossAxisAlignment : 속성으로 CrossAxisAlignment.~를 받는데 기준은 해당 축을 기준으로 함. Row내에서 정렬 시 위 아래 공간을 기준으로, Column내에서 정렬 시 좌우 공간을 기준으로.

.center는 중앙
.spaceAround는 여백을 기준으로 균일하게
