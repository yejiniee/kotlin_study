# Layout

## Constraint Layout

> 편집기 활용
<img src="https://user-images.githubusercontent.com/50178026/116395641-536ddb00-a85f-11eb-9df7-e26c00ea5199.png" width="250" height = "250">

- `동그라미`로 연결 해제 가능
- `+` 클릭하면 가장 가까이 있는 위젯 또는 레이아웃의 앵커 포인트에 컨스트레인트 생성됨
- 숫자는 연결된 위젯과의 거리를 뜻함

> wrap content : 위젯의 크기를 내용물의 크기에 맞춤  

<img src="https://user-images.githubusercontent.com/50178026/116397224-4e119000-a861-11eb-984e-791fc244eb41.png" width="90" height = "40">


> fixed : 속성에 입력된 크기로 고정  

<img src="https://user-images.githubusercontent.com/50178026/116396246-1fdf8080-a860-11eb-87b7-ad57b54f2951.png" width="90" height = "40">

> match constraint : constraint의 시작과 끝에 맞춰서 크기 조절  

<img src="https://user-images.githubusercontent.com/50178026/116396352-40a7d600-a860-11eb-9e48-2f64a3ba70b2.png" width="90" height = "40">

<img src="https://user-images.githubusercontent.com/50178026/116396397-4dc4c500-a860-11eb-9d3c-38fedf2c3c02.png" width="200" height = "300">

- 가로세로비 설정 가능

> Bias: 위치 조절 버튼

> Chaining     
> - constraint로 연결된 위젯끼리 서로 위칫값을 공유해서 상대적인 값으로 크기와 위치를 결정하도록 함   
> - chaing 하고자 하는 위젯 선택 -> `Chains`

<img src ="https://user-images.githubusercontent.com/50178026/116399713-2cfe6e80-a864-11eb-827e-dd7ca1b94036.png" width = "400" height = "220">

## Linear Layout

- 코드로 변경 가능
- component tree에서 레이아웃 우클릭 -> `convert view`  
<img src ="https://user-images.githubusercontent.com/50178026/116400288-d80f2800-a864-11eb-969c-f9cadafbd97e.png" width = "300" height = "280">

> orientation  
- horizontal: 가로로 배치  
- vertical: 세로로 배치  

> layout_weight
- 비율 설정

> gravity
- 위치 설정
```xml
 <Button
    android:id="@+id/button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:layout_weight="1"
    android:text="Button" />     
```
> scroll view
```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity" >

    <LinearLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <Button
            android:text="button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>
        <Button
            android:text="button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>
    </LinearLayout>
</ScrollView>
```
> Space   
> : 빈 여백 만듦   
```xml
<LinearLayout
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <Button
       android:text="button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"/>
    <Space
       android:layout_width="20dp"/>
    <Button
       android:text="button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"/>
</LinearLayout>
```
<br>

# Widget

## Text   
#### Text 추가

`app` -> `res` -> `values` -> `strings.xml`    
> strings.xml  
```xml
<resources>
    <string name="app_name">My Application</string>
    <string name="string_01">안뇽 1</string>
</resources>
```

> activity_main.xml
```
<Button
    android:text="@string/string_01"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```
<image src="https://user-images.githubusercontent.com/50178026/116404937-13602580-a86a-11eb-8695-def7d5682d69.png" width = "350" height = "100" >   

#### textColor
-  `app` -> `res` -> `values` -> `colors.xml`    

#### textSize
- 단위: sp 사용  
> dinems.xml  
> - values directory에 `new`->`values resource file`-> dimens 추가  
```xml
<resources>
    <dimen name="text_dimen">24sp</dimen>
</resources>
```

#### textStyle   
- normal, bold, italic 선택 가능  
- maxLines: 최대 입력 가능한 줄 수  
- minLines: 최소 입력 가능한 줄 수   
- singleLine: maxLines=1과 달리, 줄 사이의 \n 없애 한줄로 보이도록 함
- ellipsize: 문자열이 길어서 글자가 잘릴 때 말줄임 표시
  - start: 첫부분 말줄임표
  - middle: 가운데 말줄임표
  - end: 끝부분 말줄임표
- fontFamily: 글씨체 설정
- ems: 상대값
- lines: 텍스트뷰 높이 고정
- maxLength: 전체 길이 고정  

## EditText
