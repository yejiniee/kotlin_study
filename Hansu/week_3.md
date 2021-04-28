# 위젯과 리소스 다루기

레이아웃 | 설명
---------|------
Constraint Layout| 간단한 드래그 앤 드롭만으로 화면 요소들을 원하는 곳에 배치 |
Linear Layout    | 위젯을 가로 또는 세로 한 줄로 배치하기 위한 레이아웃 |
Frame Layout     | 위젯을 중첩해서 사용하기 위한 레이아웃 |


## 레이아웃

* 프로젝트를 생성시, activity_main.xml 이라는 이름의 레이아웃 파일이 자동으로 만들어짐.
* 레이아웃 파일은 소스코드가 아니라 리소스로 분류되어, 파일명은 소문자로 작성된다. (리소스 파일명은 모두 소문자)

> Constraint Layout
-----------------

* 안드로이드 기본 레이아웃(Default)
* 위젯 사이에 간단한 제약조건 설정으로 화면을 쉽게 구성할 수 있다.

#### 핸들러

* UI편집기에서 위젯을 클릭하면 나오는 상하좌우에 있는 4개의 동그라미.
* 주름무늬선(화살표) = 컨스트레인트, 컨스트레인드가 연결되는 부위 = 앵커 포인트
* 핸들러를 드래그하여 연결하고자 하는 다른 위젯의 핸들러에 가져다 놓거나, 자신을 포함하는 레이아웃의 가장자리에 놓으면 컨스트레인트가 생긴다.

### 컨스트레인트 편집기

* 위젯을 선택하면 우측 속성 영역에 컨스트레인트를 조절 할 수 있는 편집기가 나타난다.
* 핸들러를 클릭하여 연결, 연결해제 가능(연결시는 가장 가까운 앵커 포인트에 생성)
* 컨트스레인트가 가로 또는 세로 양쪽이 쌍으로 연결되면 크기 조절 핸들러와 바이어스를 사용 할 수 있다.

### 크기 조절 핸들러(Size Handler)

* 상하 또는 좌우 양쪽에 컨스트레인트가 연결 되었을 때 사용
* 우측 속성 영역에 박스 안쪽의 화살표(>> <<) 모양 클릭시 세 가지 모드로 변경

* |>> <<| (Wrap Content) : 위젯의 크기를 내용물의 크기에 맞춤.
* |-| |-| (Fixed) : layout_width, layout_height 속성에 입력된 크기로 고정.
* |-N-| |-N-| (Match Constraint) : 컨스트레인트의 시작과 끝(앵커 포인트)에 맞춰 크기 조정.
  + 매치 컨스트레인트 모드에서 값을 입력하면 해당 값 만큼 컨스트레인트의 위치가 멀어짐

### 바이어스(Bias)

* 상하 또는 좌우 양쪽에 컨스트레인트가 연결 되었을 때 활성화. 우측 속성 영역에 박스 아래에 위치. ( ------(숫자)-------)
* 위치 조절 버튼
* 가운데 숫자는 비율을 의미하며, 0~100 사이의 숫자로 위젯의 위치를 조정

### 가로세로비 설정

* 크기를 매치 컨스트레인트로 설정시 활성화. 우측 속성 영역에 박스의 좌측 위 모서리에 작은 삼각형 모양.
* 삼각형 모양 클릭시 위젯의 가로세로 비율을 설정할 수 있는 ratio필드가 나타난다. (가로 : 세로)
* 내용이 있는 위젯은 상하좌우 모두 컨스트레인트를 연결하고 ratio값을 입력하면 정상적으로 나타난다.

### 레이아웃 툴바

* 레이아웃에 따라 다른 툴바가 제공됨
1. View Option : 제약 조건을 표시/숨기기
2. Auto Connect : on상태에서 위젯을 컨스트레인트 레이아웃에 갖다 놓으면 기본 컨스트레인트를 연결
3. Default Margins : 컨스트레인트 연결 시 설정한 만큼 기본 마진 적용
4. Clear Constraints : 화면의 모든 컨스트레인트 제거, 개별로 제거시 위젯에 마우스를 올려 동일 아이콘 클릭
5. Infer Constraints : Auto Connect off시 사용. 가까운 위젯에 2개이상의 컨스트레인트 연결
6. Pack : 여러 위젯 동시 선택 상태에서 크기 조절시 사용. 위치가 조절될 때도 있음
7. Align : 선택된 위젯들을 정렬
8. GuideLine : 레이아웃 안의 모든 위젯에 공통의 여백을 지정할 때 사용. 위젯은 가이드라인에 컨스트레인트를 연결할 수 있다.

### 체인으로 연결하기

* 컨스트레인트로 연결된 위젯끼리 위치값을 공유하여 상대적인 값으로 크기와 위치를 결정해주는 것 (상대비율 유지)
* 컨스트레인트 레이아웃은 한 레이아웃에 여러 개의 위젯 구현 가능 (기존에는 여러 개의 레이아웃을 겹쳐야 했다)

1. UI 화면에서 chain 할 위젯들을 선택후 마우스 우클릭 - Chains - Create Horizontal(Vertical) Chain 선택
2. 해당 위젯 사이에 체인모양이 생성.
3. layout_width와 layout_height를 0dp(match constraint)로 바꾸면 화면에 꽉찬 크기로 바뀐다.

### 가이드 라인

* 컨스트레인트 레이아웃에서만 사용할 수 있다.
* 레이아웃 안에 배치되는 위젯에 가상의 앵커 포인트 제공


> Linear Layout
-----------------

* 위젯을 가로 또는 세로 한 줄로 배치하기 위한 레이아웃
* 레이아웃 속성 중 orientation: horizontal(가로), vectical(세로)

### 리니어 레이아웃을 기본 레이아웃으로 사용하기

* 컨스트레인트 레이아웃 안에 추가하여, 리니어 레이아웃이 중첩되면 그래픽 처리 속도가 느려짐.
  1. 속성 영역 위에 있는 [Code] 버튼을 클릭
  2. <androidx.constraintlayout.widget.ConstraintLayout ......> 에서 androidx.constraintlayout.widget.ConstraintLayout 을 LinearLayout으로 수정. 닫는 부분도 수정해야함
  3. 다시 우측 상단의 [Design] 버튼을 클릭해서 모드를 변경
  
### orientation 속성

* orientation의 default값은 horizontal(가로)이다.

### layout_weight 속성

* 레이아웃 안에 배치되는 위젯의 크기를 비율로 나타낼 수 있는 옵션. default값은 1
* layout_weight 속성값을 정확하게 주기 위해서는 layout_width,height 속성값을 0dp로 주면 된다.

### gravity 속성

* 속성 영역 하단의 All Attributes 영역에 위치 -> gravity 검색 -> 화살표를 눌러 하위 속성을 조정
* 레이아웃들의 필수 속성
* 레이아웃에 삽입되는 위젯을 설정된 방향으로 정렬, 동시에 2개 이상의 방향 설정 가능

### layout_gravity 속성

* 부모 레이아웃을 기준으로 자신의 위치를 설정
* gravity:right 하면  |...[....버튼]...|
* layout_gravity:right 하면  |.......[..버튼..]..|

### 스크롤뷰와 함께 사용하기

* 일반 레이아웃들은 화면 크기를 넘어가는 위젯이 삽입돼도 스크롤이 되지 않음, 화면에서 잘림
* 이럴때는 최상위 레이아웃을 스크롤 할 수 있는 요소로 감싸면 된다.
* 두가지 방법
1. 기본 레이아웃을 스크롤뷰로 변경해서 사용
2. 기본 레이아웃 안에 스크롤뷰를 추가한다.  
  1. 속성 영역 상단의 [Code] 클릭후 androidx.constraintlayout.widget.ConstraintLayout 을 ScrollView로 변경
  2. [Design] 모드로 변경하고, 기본으로 있는 텍스트뷰를 삭제.
  3. 팔레트 영역의 레이아웃 카테고리에 있는 Linear Layout 1개를 드래고 해서 스크롤뷰 안에 가져다 놓는다.
  4. 그 후, orientation 속성을 vertical로 변경한다.

### Space

* 빈 여백을 만들 수 있는 보조 도구
* Space: layout_width, 20dp

> Frame Layout
----------------

* 위젯을 중첩해서 사용하기 위한 레이아웃
* 게임 화면처럼 배경과 플레이어가 서로 다른 레이어에서 겹쳐 움직여야 할 때 사용
* 레이아웃중 처리 속도가 가장 빠름 -> 1개의 이미지만 사용하던지, 단순한 형태로 사용할 경우 성능이 좋다.
* 삽입되는 다른 레이아웃이나 위젯을 겹쳐놓는 용도
* 필수 속성x
* 정렬은 삽입되는 위젯의 layout_gravity 속성 사용

### Frame layout의 XML 구조

* 속성 영역 상단의 [Code] 클릭

```xml
<?xml version="1.0" encodeing="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
             android:layout_width="match_parent"
             android:layout_height="match_parent">
</FrameLayout>
```

* XML 코드는 앞뒤로 홑화살괄호(<>)로 감싼 형태로 생성
* [Design]모드로 변경 후, 팔레트에서 버튼을 드래고해서 UI편집기에 가져다 놓으면 버튼 생성
* 그 후 코드
```xml
<?xml version="1.0" encodeing="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
             android:layout_width="match_parent"
             android:layout_height="match_parent">
             //여기부터 버튼위젯에 대한 코드
             <Button
                     android:id="@+id/button"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     android:text="Button/>
</FrameLayout>
```

* <태그> : 시작 태그
* </태그> : 종료 태그
* <태그/> : 홑 태그  - 시작태그와 종료태그를 한번에 사용





  
## 디자인 요소 위젯

* 팔레트 영역의 Text, Buttons, Widgets을 살펴보자.

## 위젯의 대표 메뉴

* Common : 텍스트, 버튼, 레이아웃 등 일반적으로 많이 사용되는 것들을 모아놓은 메뉴
* Text : 글자를 화면에 나타내거나(TextView) 입력받을 수 있는(Edit Text) 위젯을 모아놓은 메뉴, Ab 아이콘에 언더바가 있으면 Edit Text Widget이다.
* Buttons : 사용자로부터 클럭 또는 터치 관련 이벤트를 받을 수 있는 위젯 모음. 버튼, 라디오버튼, 체크박스, 스위치 등
  + 스마트폰에서 순을 대는 순간 = 터치, 터치한 뒤 같은 위치에서 손가락을 떼었을 때 = 클릭
* Widgets : 이미지, 웹사이트, 별점 표시, 진행 상태등의 정보를 화면에 그리는 모음

> TextView
-----------

* 화면에 텍스트를 출력
* 레이아웃 파일에서 텍스트뷰의 text속성에 값을 직접 입력할 수도 있고, 소스코드에서 입력할 수도 있음.

### text(strings.xml)
* 화면에 나타낼 텍스트를 입력하는 속성
* strings.xml에 사용할 텍스트를 미리 정의해 놓고 가져다가 사용하는 것이 관리하기에 용이 (app-res-values-strings.xml)

```xml
//<string name="스트링 이름(공백x,중복x)">보여질 텍스트</string> / id의 용도
<resources>
  <string name="app_name">WidgetsTextView</string>
  <string name="string01">화면에 보여질 글자 01</string>
  <string name="string02">화면에 보여질 글자 02</string>
</resources>
```

* TextView에 적용하기 위해 activity_main.xml파일을 연 후, text속성의 입력필드에 '@string/string01' 형태로 입력

### textColor(colors.xml)
* 텍스트 색상을 지정하는 속성
* RGB를 기준으로 0~255의 숫자를 16진수 8자리로 입력해서 표현.
* '#투명빨강녹색파랑' 형식 (00~FF). 투명은 00에 가까울 수록 투명, 나머지는 FF에 가까울 수록 해당색에 가까워진다. 투명값이 없으면 투명빼고 6자리만 입력
* colors.xml에 작성한 뒤 값을 참조해서 사용. (app-res-values) values가 없으면 메뉴에서 [New]-[Value Resource File]을 선택해 생성
  + colors.xml에는 기본 컬러기 이미 있다. <color name="컬러이름">#색상</color> 형식 <!-- 새로추가 --> 와같은 주석을 달고 추가하자
* 적용시에는 TextView의 속성의 textColor에 '@color/컬러이름'을 입력

### textSize(dimens.xml)
* 텍스트의 크기를 지정하는 속성
* dp, px, sp등의 단위 사용. 텍스트는 이중에서 sp(Scale-independent Pixels)를 사용. 다른위젯은 대부분 dp사용
  + sp를 사용하는 이유는 같은 해상도에서 문자열의 크기를 다르게 사용하는 경우가 있기 때문. 화면 스케일에 독립적으로 크기를 조절할 수 있는 단위
  + 눈이 안 좋은 사람이 폰트 크기를 키워야할 때, sp를 이용하면 다른 위젯에 영향x
* dimens.xml을 참조하여 사용. values디렉터리에서 따로 만들어서 사용한다. values디렉터리 우클릭 - New-Values-Resource File, File name : dimens
* <dimen name="단위이름"?150sp</dimen> 형태로 작성
* 사용시는 textSize 속성 입력필드에 '@dimen/단위이름' 입력

### textStyle
* 텍스트의 스타일을 설정하는 속성
* normal, bold(굵게), italic(기울임) 중복가능

### maxLines, minLines
* 입력 가능한 최대/최소 줄 수 설정
* minLines는 줄이 입력되면 자동으로 높이가 늘어난다.

### singleLine
* 텍스트뷰를 한 줄로 보이게하는 속성(줄 사이의 \n을 없앤다)

### ellipsize
* 문자열이 길어서 글자가 잘릴 때 말줄임(...) 표시를 하거나, marquee로 글자를 좌우로 움직이게 한다.
  + none: 설정하지않습니다
  + start: 텍스트의 첫 부분을 바꿈
  + middle: 중간 부분을 바꿈
  + end: 끝 부분을 바꿈
  + marquee: 글자가 흐르는 효과.(singleLine을 true로 설정해야 사용가능. focusable은 auto, focusableInTouchMode속성은 true로 설정하면 전광판효과)

### fontFamily
* 글꼴을 지정하는 속성. 외부 폰트도 지정가능.
* 입력필드 클릭 후 More Fonts로 글꼴 추가

### ems
* 현재 글꼴의 크기를 기준으로 글꼴 크기 설정
  ex) 현재 텍스트뷰의 크기가 12sp라면, 1em = 12sp, 2em = 24sp
  + 즉, 텍스트와 텍스트뷰의 비율 유지하기 위한 것

### lines
* 텍스트뷰의 높이를 고정할 때 사용

### maxLength
* 텍스트의 전체 길이를 제한하는 속성. 나머지는 보이지 않게한다.


> EditText
----------

* 텍스트 카테고리의 Plain Text부터 Number(Decimal)까지 이름 앞에 Ab아이콘이 붙어있는 것이 모두 EditText위젯이다.
* 글자를 보여주기도 하지만, 주로 입력받는 용도로 사용
* Textview의 주요 속성을 거의 그대로 사용하고 입력받는다.

### 입력되는 글자를 실시간으로 처리하기
* 입력되는 글자를 실시간으로 로그에 출력하기
  + activity_main.xml파일을 열고 PlainText를 텍스트뷰 아래에 놓는다.
  + id속성 입력필드에 editText를 입력한다.
  + text속성에 기본값을 삭제한다.(Common Atributes)
  + bundle.gradle파일을 열고 android스코프에 viewBinding true설정을 추가. 추가 후, Sync Now클릭
  ```xml
  //이 코드는 외워두자
  buildFeatures {
    viewBinding true
  }
  ```
  + MainActivity.kt로 이동. class MainActivity에 binding프로퍼티를 하나 생성하고 by lazy를 사용해서 ActivityMainBinding을 inflate한다.
  ```kotlin
  //2장의 2.5 코틀린코드와 레이아웃 연결하기 참조
  class MainActivity: AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }
  ```
  + onCreat() 메서드 안에 setContentView에 binding.root를 전달한다.
  + 이어서 binding으로 앞에서 작성해둔 에디트텍스트의 id에 연결한다.
  ```kotlin
  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(binding.root)
    binding.editText.addTextChangedListener { // EditText의 변경사항을 캐치할 리스너를 달아야 한다. 
      Log.d("EditText", "현재 입력된 값=${it.toString()}")
    }
  }
  ```
  + 이후 run App 아이콘으로 실행.

* 한글 키보드 설정법
  + 에뮬레이터 화면 하단을 클릭 후, Settings -> System -> Languages & Input -> Languages(English)선택 -> Add a language -> 돋보기 -> Korean입력 후 선택

### hint
* 클릭하면 사라지는 미리보기 (place holder라고도 불림)

### inputType
* 키보드 모양 설정
* number - 숫자만 있는 키보드, texPassword - 입력되는 텍스트가 검은색 점으로 가려짐 등

### imeOptions
* 입력 완료 후 실행할 이벤트 설정 (input method editor)


> 이미지 버튼
------------
* 버튼은 이미지 위에 텍스트만 가능, 이미지버튼은 이미지 위에 이미지 가능
* 리스너를 텍스트에 구현했느냐, 이미지뷰에 구현했느냐의 차이
* 이미지 뷰의 속성을 그대로 사용한다.

### 기본 이미지 사용
* activity_main.xml의 UI편집기에 이미지버튼을 가져다 놓으면 이미지 선택창이 나욤 -> Drawable클릭하면 sample data가 나옴

### 새 이미지 사용
* 사용할 이미지를 준비해서 drawable 디렉터리에 붙여넣기 한 다음 Refactor
* 팔레트에서 이미지버튼을 드래고해서 UI편집기에 가져가놓는다. 그 후, 속성영역의 src 옆 버튼을 클릭하여 붙여넣기한 이미지를 선택

### 투명배경 설정
* 속성 중 background 속성에 '@android:color/transparent'를 적용

### scaleType
* 이미지 크기 설정, 이미지뷰에서도 사용

### tint
* 이미지 영역에 색을 채우는 속성. 스포이드 아이콘을 클릭해서 색선택
* 이미지의 투명도를 기준으로 색이 적용된다.

### alpha
* 투명도를 조절. (0~1) 0이면 투명


> RadioGroup & RadioButton
-------------------------
* activity_main.xml -> 버튼카테고리 -> 라디오그룹 -> id 속성에 radioGroup 입력
* 컴포넌트 트리에서 radioGroup을 찾아 클릭
* 라디오그룹안에 라디오버튼을 가져다 놓는다. 각각 id속성을 정해준다.
* 라디오버튼의 text속성에 화면에서 볼 수 있는 텍스트를 입력
* bundle.gradle파일을 열고 android스코프에 viewBinding true 설정 추가 -> Sync now
```xml
buildFeatures {
  viewBinding true
}
```

* MainActivity.kt 클릭 후 onCreate()메서드 위에 binding프로퍼티생성 후 ActivityMainBinding을 inflate
```kotlin
  val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }
```
* onCreate() 안에 작성되어 있는 setContentView에 binding.root 전달
```kotlin
setContentView(binding.root)
binding.radioGroup.setOnCheckedChangeListener { group, checkedId ->
  when (checkedID) {
  //R.id.radioApple -> Lodg.d~
  //~~코드
  }
}
```

### oriendtation
* 라디오그룹은 리니어 레이아웃에 라디오버튼을 담을 수 있는 형태의 레이아웃.
* 라디오버튼들을 가로로 정렬할지 세로로 정렬할지 정할 수 있다.

### checkedButton
* 미리 선택되어 있는 라디오버튼 설정

> 체크박스
----------
* 라디오버튼과 달리 여러개 선택가능
* 공통으로 사용되는 리스너 1개만 구현해서 사용가능
  
* 리니어 레이아웃을 가운데 배치, 체크박스를 리니어 레이아웃 안에 놓고 id와 text값 입력
* layout_width,height를 wrap_content로 설정
* build.gradle에 viewBinding true 추가
* MainActivity.kt 탭에서 onCreate() 위에 binding 프로퍼티생성 후 ActivityMainBinding을 inflatae
* onCreate()안의 setContentView에 binding.root전달
```kotlin
binding.checkid.setOnCheckedChangeListener { buttonView, isChecked ->
  if(isChecked) Log.d(~~)
  else Log.d~~
}
```
* 위의 방식은 모든 체크박스에 리스너를 달아줘야함. 불편
* 밑의 방식사용
```kotlin
class MainActivity : AppCompatActivity() {
  val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }
  val listener by lazy {
    CompoundButton.OnCheckedChangeListener { buttonView, isChecked ->
      if (isChedcked) {
        when (buttonView.id) {
        R.id.checkApple -> ...
        //...
        }
      } else { //체크버튼이 해제되었을 때
        when(buttonView.id) {
        //...
        }
      }
    }
  }
  
  override fun onCreate(saveInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(binding.root)
    
    binding.checkid.setOnCheckedChangeListener(listener)
    binding.checkid2.setOnCheckedChangeListener(listener)
    binding.checkid3.setOnCheckedChangeListener(listener)
```

> 토글버튼, 스위치, 이미지뷰
---------------------------
* 토글버튼: 체크박스와 동일. CompoundButton을 상속받아 사용하기때문에 동일. 모양만 조금 다르다.
* 스위치: 체크박스와 동일, CompoundButton을 상속받아 사용(체크박스도 이것을 상속받아사용)
* 이미지뷰: 이미지버튼과 사용법 유사. 리스너를 달아서 clock 이벤트도 받을 수 있지만, 이미지를 보여주는 용도로만 사용하자.

> ProgressBar
-------------
* 진행 상태를 나타내는 위젯

### 진행상태표시하기
* 리니어레이아웃 id 속성에 progressLayout입력. gravity는 center
* 팔레트 위젯 카테고리에서 프로그레스바와 텍스트뷰를 리니어 레이아웃에 놓는다. 텍스트뷰의 gravity도 center
* build.gradle파일에 viewBinding설정
* MainActivity.kt 탭에서 binding생성 후 setContentView에 bindinf.root전달
* 클래스안(Oncreate밖)에 showProgress 메서드를 만들고 리니어 레이아웃을 숨겼다 보였다 할 수있는 코드 추가
```kotlin
fun showProgress(show: Boolean) {
  if (show) { //INVISIBLE은 안보이는 상태(공간은 차지함), GONE은 안보이는 상태인데 공간도 차지안함
    binding.progressLayout.visibility = Vew.VISIBLE
  } else {
    binding.progressLayout.visibility = View.GONE
  }
}
```
* 그림그리는 코드는 메인스레드에서만 실행할 수 있음.(UI Thread라고도함)
* onCreate()안의 코드는 모두 메인스레드에서만 그려짐.
* 이를 위해서 thread(start=true) 사용
```kotlin
thread(start=true) {  //서브스레드
  Thread.sleep(3000)
  runOnUiThread {   //메인스레드
    showProgress(false)
  }
}
```

> SeekBar
--------
* 볼륨을 조절하거나 재생시간을 조절하는 용도로 사용

* 위젯 카테고리의 SeekBar를 가져다놓는다. layout_width:0dp, height:wrap_content
* id속성에 seekBar입력
* seekBar위에 텍스트보ㅠ를 하나 가져다 놓고 컨스트레인트 연결
* build.gradle에 viewBinding설정 후 MainActivity.kt에서 binding.root전달
* setContentView 아랫줄에 binding.seekBar.setOnSeekBarChangeListener 선택
* 리스너의 중괄호 안에 마우스를 두고 Ctrl + I 키를 입력 후 Implement Members 팝업창에서 3개의 메서드를 모두 선택 후 OK클릭
* 각 메서드의 TODO행은 삭제한다. 혹은 주석처리
```kotlin
binding.seekBar.setOnSeekBarChangeListener(object: SeekBar.OnSeekBarChangeListener {
  override fun onProgressChanged(seekBar: SeekBar?, progress: Int, fromUser: Boolean) {
    binding.textView.text = "$progress"
  }
  override fun onStartTrackingTouch(seekBar: SeekBar?) {
    //ToDo~~
  }
  override fun onStopTrackingTouch(seekBar: SeekBar?) {
    //ToDo~~
  }
})
```
* 주요 속성 - max:시크바의 최대값 설정. progress: 처음시작하는 시크바의 값 설정

> RatingBar
-------------
* 별점을 매기는 위젯
* RatingBar를 화면에 놓는다.
* 레이팅바 오른쪽에 텍스트뷰 배치후 컨스트레인트를 레이팅바와 연결
* build.gradle파일에 viewBinding 후 MainActivity.kt에서 binding.root
* setContentView 다음줄에
```kotlin
binding.ratingBar.setOnRatingBarChangeListener { ratingBar, rating, fromUser ->
  binding.textView.text = "$rating"
}
```
* rating: 현재 별점
* fromUser: 사용자 입력 여부
* 주요속성 : numStars-전체 표시되는 별의 개수 설정, rating-처음시작하는 별점값, stepSize-별을 드래그 했을때 움직이는 최소 단위 (0~1)
* 각 속성에 도트연산자로 값을 입력 가능

* 인터페이스에 정의되어 있는 메서드가 1개면 중괄호를 사용하여 코드 축약 가능(람다식)


## 리소스 다루기

* 이미지 리소스인 drawable, 앱 아이콘에 사용되는 mipmap, 그리고 strings를 이용한 다국어 처리에 대해 알아보자

> drawable과 단위
-----------------
* 스마트폰마다 화면의 픽셀수가 다르기 때문에 사이즈를 표시하는 단위로 가상화소 개념인 dp를 사용.
* dp는 화면밀도(DPI)에 따라서 실제 픽셀로 변환되는 크기가 달라진다.

### DPI

표현 | 화소수 | 비고
-----|-------|-----
ldpi | 120   | 현재사용하지않음
mdpi | 160   | 기준: 1dp = 1pixel
hdpi  | 240  |
xhdpi | 320  | 1dp - 2pixel
xxhdpi| 480  | 1dp = 3pixel
xxxhdpi| 640 | 1dp = 4pixel

* 가로세로 1인치의 공간에 들어 있는 펙셀수를 나타내는 단위.
* 기본은 160dpi 인데 이를 mdpi라고 한다.

### dp
* density-independent Pixels. 안드로이드에서 사용하는 독립적 수치 단위.
* 해상도와 관계없이 동일한 크기로 화면에 표시

### sp
* Scale-independent Pixels
* 문자열의 크기를 나타내기 위해 사용하는 단위
* 줌인, 줌아웃 시에 다른위젯에 영향x

### drawable 디렉터리 구성
* DPI구조로 인해 해상도에 맞는 drawable 디렉터리에 이미지를 넣고 사용해야 한다.
* DPI별 디렉터리를 수동으로 생성하려면 Project뷰에서 res 디렉터리를 마우스 우클릭 -> New -> Directory선택 후 이름입력
* 안드로이드는 호출된 이름을 확인 후 해상도에 맞는 디렉터리 안의 이미지를 사용한다.
* drawable-v24 디렉터리는 디바이스버전 24이상일때 자동으로 선택됨
* 뒤에 접미사가 없는 drawable 디렉터리는 이미지 외에 화면과 관련된 XML파일을 관리하는 용도로 사용
* 이미지 표현방식은 비트맵(사진)과 벡터(아이콘) 방식이 있음

> mipmap 앱 아이콘
------------------

### mipmap
* 앱 아이콘에 사용되는 디렉터리. 일반이미지는 drawable에 넣자.
* 각각의 디렉터리에 (mipmap-anydpi-v26, mipmap-hdpi, mipmap-mdpi 등) 아이콘 이미지를 넣고 AndroidManifest.xml에 있는 <application>태그의 icon속성에 설정하면 앱 설치 후 안드로이드 화면에 나타난다.
```xml
  <application
               android:allowBackup="true"
               android:icon="@mipmap/ic_launcher"
               android:label="Camera And Gallery"
               android:roundIcon="@mipmap/ic_launcher_round" //roundIcon속성은 25버전부터 지원. 런처가 동그란 아이콘을 사용하면 이 속성의 이미지 사용
```

### adaptive icon
* mipmap-anydpi-v26 디렉터리 안에 ic_launcher.xml파일을 열어보면 백그라운드 이미지와 포어그라운드 이미지 2개를 포개어서 아이콘으로 그려주는 역할을 한다.
```xml
  <?xml version="1.0" encoding="utf-8"?>
  <adaptive-icon xmlns:android="http://schemas.android.com/apk/res/android">
    <background android:drawable="@drawable/ic_launcher_background" />
    <foreground android:drawable="@drawable/ic_launcher_foreground" />
</adaptive-icon>
```
* @drawable/ic_launcher_background 파일명이 지정되어 있는데, 벡터 기반의 이미지가 입력되어 있다. 이런 구조를 adaptive icon이라고 한다.
* 이미지 아이콘과 동일하게 AndroidManifest.xml에 있는 <application>태그의 icon 속성에 적용하고 사용

> strings와 다국어 처리
-----------------------

### string
* strings.xml을 Translations Editor를 통해서 관리 가능
  + strings.xml을 열으 Open editor 클릭
  + Translation Editor가 나타나는데, Code모드에서 XML을 수정하는 대신에 에디터를 통해 strings를 추가 삭제할 수 있다
  + 에디터상단의 [+]버튼을 클릭하면 <string>태그 생성할 수 있는 팝업창이 나타난다.
  + [-]버튼은 <string>을 삭제하는데 사용.

### 다국어 처리하기
* Translations Editor는 다국어를 처리하는게 목적이다.
* 지구본을 클릭하면 선택메뉴에서 [Korean(ko)]선택.
* 기존 strings목록 칼럼에 Korean(ko)가 추가됨. 좌측 탐색기에는 values-ko가 생성되어 있고, 그 안에 strings.xml이 추가되어 있다.
* Translations Editor에서 Korean(ko) 칼럼에 한글 입력
* 입력 완료 후 strings.xml(ko)파일을 열어보면 설정이 완료되어있음.
* Translations Editor를 이용해서 국가별 strings.xml파일을 구성하여 사용.
