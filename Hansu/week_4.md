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
