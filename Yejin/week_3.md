# 레이아웃
## 컨스트레인트 레이아웃
간단한 드래그만으로 각각의 화면 요소들을 원하는 곳에 배치할 수 있다.
* 체인으로 연결하기: 위젯선택->우클릭->[chains]->[ceate chain]

## 리니어 레이아웃
위젯을 가로 또는 세로 한 줄로 배치하기 위한 레이아웃이다.
* 스크롤 뷰와 함께 사용하기:
기본 레이아웃을 스크롤뷰로 변셩한 후 스크롤 뷰 안에 리니어 레이아웃을 넣는다.

## 프레임 레이아웃
입력되는 위젯의 위치를 결정하기 보다는 위젯을 중첩해서 사용하기 위한 레이아웃

# 위젯
## Buttons
사용자로부터 클릭 또는 터치 관련 이벤트를 받을 수 있는 위젯의 모음.
버튼, 라디오버튼, 체크박스, 스위치가 여기에 속한다.

## 텍스트뷰
- textColor: 텍스트 색상 지정
#FFFFFFFF(흰색) #FF888888(회색) #FFFF0000(빨간색)\

- textSize: 텍스트 크기 지정
텍스트뷰, 에디트텍스트에서는 주로 sp를 사용.
>dimens.xml 파일에 저장해서 사용하기

[values]->우클릭->[New]->[Values resource file]->file name: dimens

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <dimen name="text_dimen">24sp</dimen>
    <dimen name="size_dimen">24dp</dimen>
</resources>
```

<img width="213" alt="git_1" src="https://user-images.githubusercontent.com/80842764/116807095-2f1a4300-ab6c-11eb-8260-722f181715e5.PNG">

- textStyle: 텍스트 스타일 지정. normal, bold, italic 세가지가 있음.

- maxLines, minLines: 입력가능한 줄 수 설정하기

maxLines: 최대 입력 가능한 줄 수 설정. 그 이상은 출력되지 않는다.

minLines: 최소 줄 수를 미리 설정해두어 글자의 입력여부와 관계없이 최소 공간을 미리 마련해둠

- singleLine: 텍스트가 여러 줄이 있을 때 한줄로 보여줌

- ellipsize: 말줄임표시하기. maxLine 속성이 1이거나, 문자열이 길어서 글자가 잘릴 때 설정함   

-none: 설정하지 않는다   

-start: 첫부분 말줄임표   

-middle: 중간부분 말줄임표   

-end: 끝부분 말줄임표   

-marquee: 글자가 흐르는 효과를 줌   

- fontFamily: 텍스트 글꼴 지정
- ems: 비율로 글꼴 크기 지정

텍스트뷰의 크기를 나타낼 때 현재 글꼴의 크기를 기준으로 설정하는 상대값. ex) 현재 설정된 크기가 12sp라면, 1em=12sp, 2em=24sp

- lines: 텍스트뷰 높이 고정. 텍스트가 늘어나거나 줄어들어도 공간은 변하지 않음.

- maxLength: 텍스트 전체 길이 제한

**참고-주석처리하는 방법**

*<!- 주석처리할 내용->*


## 에디트텍스트
- hint: 클릭하면 사라지는 미리보기
- inputType: 키보드 모양 설정하기

|inputType|옵션값|
|-----|-----|
|textUri|URI 형식의 문자 입력|
|textEmailAdress|email 형식의 문자 입력|
|textPostalAdress|우편번호 형식의 문자 입력|
|textPassword|비밀번호 입력|
|textVisivlePassword|비밀번호를 문자열 그대로 표시하기|
|number|숫자형식|
|numberPassword|숫자로만 구성된 비밀번호 입력|
|phone|전화번호 형식|
|date|날짜 형식|

- imeOptions: 이벤트 설정하기
- 
입력 완료 후 실행할 이벤트를 설정. Ime(imput method editor): 텍스트 편집기

## 이미지버튼
*버튼과 이미지버튼의 차이*

버튼: 이미지 위에 텍스트. 텍스트뷰의 속성

이미지버튼: 이미지 위에 아이콘과 같은 이미지 추가 가능. 이미지뷰의 속성

-기본 이미지 사용

[이미지버튼]을 UI편집기에 드래그->원하는 이미지 선택

-새로운 이미지 사용

원하는 이미지를 drawable 디렉터리에 드래그 앤 드롭 한 뒤 drawable 뒤의 -v24를 지우고 저장 한 뒤 src에서 다시 이미지 선택

<img width="678" alt="git_2" src="https://user-images.githubusercontent.com/80842764/116808068-d6e63f80-ab71-11eb-891c-6c000db460fb.PNG">

- scaleType: 이미지 크기 설정하기

|scaleType|기능|
|-----|--------|
|matrix|좌측 상단부터 이미지버튼 크기만큼만 보여준다.|
|fitXY|상하좌우를 이미지버튼 크기에 맞춰 늘려준다.|
|fitStart|좌측 상단부터 시작해서 비율에 맞게 이미지 크기를 조절하여 위젯 안에 채워준다.|
|fitCenter|중앙을 기준으로 비율에 맞게 이미지 크기를 조절하여 위젯 안에 채워준다.|
|fitEnd|우측 하단부터 시작해서 비율에 맞게 이미지 크기를 조절하여 위젯 안에 채워준다.|
|center|실제 이미지 사이즈대로 정중앙에 위치시킨다. 이미지가 위젯보다 크면 위아래가 잘릴 수 있다.|
|centerCrop|가로세로 사이즈 중 근접한 길이를 기준으로 나머지 한 쪽을 잘라서 비율을 맞춰준다. 뷰에 이미지가 가득 참|
|centerInside|이미지가 위젯보다 크면 fitCenter와 같이 동작하고, 작으면 위젯의 중앙에 위치시킨다.|

- tint: 이미지 영역에 색 채우기
- alpha: 투명도 조절

1~0사이의 값을 입력. 1: 불투명, 0: 투명

## 라디오그룹과 라디오버튼
라디오 버튼: 여러 개의 선택지 중에서 하나만 선택할 때 사용.

<img width="171" alt="git_3" src="https://user-images.githubusercontent.com/80842764/116808571-7573a000-ab74-11eb-8ae1-3f9afa06cf92.PNG"> , <img width="191" alt="git_4" src="https://user-images.githubusercontent.com/80842764/116808642-e4e98f80-ab74-11eb-9d8b-6258251ef78c.PNG">
- orientation: 라디오 버튼 배치하기

선택지를 가로로 정렬할 건지 세로로 정렬할 건지 결정

- checkedButton: 미리 선택된 라디오버튼 설정하기

## 체크박스

여러개를 한번에 선택할 때 사용

<img width="173" alt="git_5" src="https://user-images.githubusercontent.com/80842764/116808729-6f31f380-ab75-11eb-8820-53142d5aff73.PNG">

기본적으로 1개의 위젯당 1개의 리스너를 달아줘야하지만 공통으로 사용되는 리스너 1개만 구현해서 사용가능

## 토글버튼, 스위치, 이미지뷰
- 토글버튼: 체크박스와 동일. 화면에 나타나는 모양만 다름
- 스위치: 체크박스와 구현이 동일.
- 이미지뷰: 이미지버튼과 사용법이 유사함. 리스너를 달아서 클릭 이벤트도 받을 수 있음.

## 프로그래스바
진행상태를 나타내는 위젯. '현재 진행 중'임을 보여주거나 얼마정도 진행됐는지 진척도를 %로 보여줌.

<img width="170" alt="git_6" src="https://user-images.githubusercontent.com/80842764/116808847-f0898600-ab75-11eb-9c69-c42a4c6fe54e.PNG"> , <img width="161" alt="git_7" src="https://user-images.githubusercontent.com/80842764/116808849-f8492a80-ab75-11eb-87e8-d0561b38d568.PNG">

## 시크바
볼륨을 조절하거나 뮤직플레이어에서 재생 시간을 조절하는 용도로 사용.

## 레이팅바
별점을 매기는 위젯


## 리소스다루기
- drawable
안드로이드는 

- DPI: 가로세로 1인치의 정사각형 공간에 들어있는 픽셀의 숫자를 나타내는 단위.
안드로이드는 160DPI를 기본으로 사용하는데 이를 mdpi라고 한다.(스마트폰의 DPI가 mdpi면 가로세로 1인치의 사각형 안에 160개의 화소 존재)
|표현|1인치 안의 화소수|비고|
|---|---|-----|
|mdpi|160|기준:1dp=1pixel|
|hdpi|240||
|xhdpi|320|1dp=2pixel|
|xxhdpi|480|1dp=3pixel|
|xxxhpdi|640|1dp=4pixel|
1인치 안의 화소수가 높을 수록 화면 밀도가 높기 때문에 선명하다.

각각의 해상도에 맞는 drawble 디렉터리에 이미지를 넣고 사용해야한다. 

<img width="140" alt="git_8" src="https://user-images.githubusercontent.com/80842764/116809033-254a0d00-ab77-11eb-9c90-d79306a75884.PNG">

- dp
안드로이드에서 사용하는 독립적 수치 단위. 해상도와 관계없이 동일한 크기로 화면에 표시됨.

- mipmap
안드로이드 앱의 아이콘에 사용된다. 

- adaptive icon
백그라운드 이미지와 포어그라운드 이미지 2개를 포개어서 아이콘으로 그려주는 역할을 한다.

- strings 다루기
안드로이드는 strings.xml을 Translations Editor를 통해 관리할 수 있다.
strings.xml을 열어 우측 상단에 있는 [Open Editor] 링크를 클릭하면 Translations Editor가 나타나는데 이 에디터를 통해 strings를 추가하거나 삭제할 수 있음

<img width="260" alt="git_11" src="https://user-images.githubusercontent.com/80842764/116809301-3d6e5c00-ab78-11eb-8c02-3539f6b9d103.PNG">

- 다국어 처리
Translations Editor의 원래 기능은 다국어를 처리하는 데 목적이 있다.

지구본 모양 아이콘을 클릭하면 여러나라가 나온다. 그 중 원하는 국가를 선택하여 사용한다.

<img width="467" alt="git_9" src="https://user-images.githubusercontent.com/80842764/116809172-bae59c80-ab77-11eb-9fa8-01bbd5a20998.PNG">

<img width="126" alt="git_10" src="https://user-images.githubusercontent.com/80842764/116809233-f97b5700-ab77-11eb-89df-823a2f716253.PNG">


