# 액티비티
## 인텐트
액티비티를 실행하기 위해선 기본적으로 인텐트가 필요하다.

#### 액티비티 전환하기
패키지명 우클릭->[New]->[Activity]->[Empty Activity]->서브 액티비티 생성

```kotlin
class MainActivity : AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent= Intent(this, SubActivity::class.java)
        binding.btnStart.setOnClickListener{startActivity(intent)} //btnStart는 버튼의 id이다.
    }
}
```

#### 액티비티 사이에 값 주고받기
```kotlin
class SubActivity : AppCompatActivity() {
    val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        binding.to1.text=intent.getStringExtra("from1")
        binding.to2.text="${intent.getIntExtra("from2",0)}" 
        //텍스트뷰의 text 속성은 문자열만 받을 수 있기 때문에 ${}을 사용해 문자열로 바꿔줌
    }
}
```

#### 메인액티비티에서 값 돌려받기
서브액티비티가 종료되면 메인 액티비티로 값을 돌려주는 코드

```kotlin
class MainActivity : AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent= Intent(this, SubActivity::class.java)
        intent.putExtra("from1", "hello Bundle")
        intent.putExtra("from2", 2020)
        binding.btnStart.setOnClickListener{startActivityForResult(intent,99)}
    }
    //cntrl+O -> [onActivityResult]
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if(resultCode == Activity.RESULT_OK){
            when (requestCode) { //서브액티비티에 입력한 값을 메인액티비티에 돌려줌
                99 -> {
                    val message = data?.getStringExtra("resultValue")
                    Toast.makeText(this, message, Toast.LENGTH_LONG).show()
                }
            }
        }
    }
}
```
## 액티비티 생명주기

#### 액티비티 생명주기 메서드

|호출되는 메서드|액티비티 상태|설명|
|----|----|--------|
|onCreate()|만들어짐|액티비티가 생성된다.|
|onStart|화면에 나타남|화면에 보이기 시작한다.|
|onResume|화면에 나타남|실제 액티비티가 실행되고 있다.|
|onResume|현재 실행중|onResume이 호출되었다면 실행중이라는 의미이다.|
|onPause|화면이 가려짐|액티비티 화면의 일부가 다른 액티비티에 가려진다.|
|onStop|화면이 없어짐|다른 액티비티가 실행되어 화면이 완전히 가려진다.|
|onDestroy|종료됨|종료된다.|

이 메서드들은 override를 통해서 사용된다.
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
}

override fun onStart() {
        super.onStart()
}

//나머지도 onStart()와 같다
```

#### 생명주기 콜백
1. 액티비티는 onCreate() 메서드로 생성된 다음 화면구성요소를 메모리에 로드하고, onStart()와 onResume()에서 화면의 구성요소를 나타내고 사용자와 상호작용한다.
2. 뒤로가기를 하거나 finish()메서드로 액티비티를 종료하면 onPause()와 onStop()이 동시에 실행되고, onDestroy()가 호출되면서 액티비티가 메모리에서 제거된다.
3. 액티비티를 종료하지 않고 새로운 액티비티를 실행하면 현재 액티비티의 생명주기가 onPause()와 onStop()까지만 호출되고 종료되지는 않는다.   그리고 새로 생성된 액티비티는 onStart()와 onResume()를 연속적으로 호출한 후 실행 상태가 된다.
4. 새로운 액티비티가 현재 액티비티를 모두 가리지 않고 생성될 때는 현재 액티비티가 onPause()까지만 진행된 후 Paused 상태에서 대기하고, 새로 생성됐던 액티비티가 종료되면 onStart()를 거치지 않고 onResume()이 호출된다.

#### 액티비티 백스택(Back Stack)
백스택은 액티비티 또는 화면 컴포넌트를 담는 안드로이드의 저장공간이다.

액티비티 A, B, C를 순서대로 실행하면 액티비티가 순서대로 화면(백스택)에 쌓이고, 사용자는 가장 위에 있는 액티비티 C를 보게 된다.

#### 태스크와 프로세스
태스크(Task)는 애플리케이션에서 실행되는 프로세스(Process)를 관리하는 작업 단위이고 프로세스는 애플리케이션의 실행단위이다.

하나의 앱을 만들고 실행하면, 앱당 하나의 프로세스가 생성되고 액티비티를 처리한다.

#### 액티비티 태스크 관리하기
> 매니페스트의 설정으로 관리하는 방법

AndroidManifest.xml에 작성되는 activity 태그 안에 속성으로 사용
```kotlin
<activity android:name=".MainActivity" android:launchMode="singleInstance"></activity>
    //<activity> 태그 안에 사용할 때는 모든 속성명 앞에 android:가 붙어야 한다.
```

|속성|설명|
|----|-----------------|
|tastAffinity|기본값은 manifest에 정의된 패키지명으로 기본적으로 한 앱의 모든 액티비티는 동일한 affinity를 가진다. 입력값은 패키지명과 같은 형태이다.|
|launchMode|호출할 액티비티를 새로 생성할 것인지 재사용할 것인지를 결정한다. 기본값은 항상 새로 설정. 네가지 모드가 있다.(standard, singleTop, singleTask, singleInstance)|
|allowTaskReparenting|호출한 액티비티를 동일한 affinity를 가진 태스크에 쌓이도록 한다.|
|clearTaskOnLaunch|true면 액티비티가 재실행될 때 실행된 액티비티의 수와 관계없이 메인 액티비티를 제외하고 모두 제거한다. 기본값은 false|
|alwaysRetainTaskState|기본 설정값이 false면 사용자가 특정 시간 동안 앱을 사용하지 않을 경우 시스템이 메인 액티비티를 제외한 액티비티들을 제거한다. true일 경우는 시스템이 관여하지 않는다.|
|finishOnTaskLaunch|앱을 다시 사용할 때 기존 액티비티를 종료할지 여부를 결정한다. 기본값이 false일 경우 종료하지 않는다.|

> 소스코드에서 startActivity() 메서드에 전달하는 플래그 값으로 관리하는 방법
```kotlin
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
```
|플래그|설명|
|----|-----------------|
|FLAG_ACTIVITY_CLEAR_TOP|호출하는 액티비티가 스택에 있으면 해당 액티비티를 Top으로 이동시키기위해 그 위에 존재하던 액티비티를 모두 삭제한다.|
|FLAG_ACTIVITY_MULTIPLE_TASK|호출되는 액티비티를 메인으로하는 새로운 태스크를 생성한다.|
|FLAG_ACTIVITY_NEW_TASK|새로운 태스크를 생성하여 생성된 태스크 안에 액티비티를 추가할 때 사용한다.|
|FLAG_ACTIVITY_SINGLE_TOP|호출되는 액티비티가 Top에 있으면 해당 액티비티를 다시 생성하지 않고 존재하던 액티비티를 다시 사용한다.|

# 컨테이너: 목록만들기
## 스피너 (Spinner)
여러개의 목록 중에 하나를 선택할 수 있는 선택도구. 스피너의 내부는 복수의 데이터를 처리할 수 있는 컨테이너 구조로 되어있다.

#### 스피너로 보는 어댑터의 동작 구조
```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        var data = listOf("- 선택하세요 -","1월","2월","3월","4월","5월","6월")
        var adapter = ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, data)
        binding.spinner.adapter=adapter //어댑터를 스피너에 연결
        //스피너를 선택하면 선택결과를 보여주는 코드
        binding.spinner.onItemSelectedListener=object : AdapterView.OnItemSelectedListener{
            override fun onNothingSelected(parent: AdapterView<*>?) {
            }

            override fun onItemSelected(
                parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
                binding.result.text=data.get(position)
            }
        }
    }
}
}
```
<img width="160" alt="git_1" src="https://user-images.githubusercontent.com/80842764/116974507-33c03200-acf9-11eb-9ad4-d82e823f981a.PNG">,   <img width="165" alt="git_2" src="https://user-images.githubusercontent.com/80842764/116974402-0b383800-acf9-11eb-9edc-5e94f93fcfe5.PNG">

선택 전 -----------------> 선택 후

## 리사이클러뷰
목록을 표시하는 컨테이너. 리사이클러뷰는 리사이클러어댑터라는 메서드 어댑터를 사용해 데이터를 연결한다.

#### 리사이클러뷰 
>MainActivity.kt
```kotlin

class MainActivity : AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        fun loadData():MutableList<Memo>{
            val data: MutableList<Memo> = mutableListOf()

            for(no in 1..100){
                val title ="이것이 코틀린 안드로이드다 ${no+1}"
                val date = System.currentTimeMillis()
                var memo=Memo(no, title, date)
                data.add(memo)
            }
            return data;
        }

        val data:MutableList<Memo> = loadData()
        var adapter = CustomAdapter()
        adapter.listData = data
        binding.recyclerView2.adapter =adapter
        binding.recyclerView2.layoutManager=LinearLayoutManager(this)

    }
}
```

> CustomAdapter.kt
```kotlin

class CustomAdapter : RecyclerView.Adapter<Holder>(){
    var listData = mutableListOf<Memo>()

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): Holder {
        val binding = ItemRecyclerBinding.inflate(LayoutInflater.from(parent.context), parent, false)
        return Holder(binding)
    }
    override fun getItemCount(): Int {
        return listData.size
    }

    override fun onBindViewHolder(holder: Holder, position: Int) {
        val memo = listData.get(position)
        holder.setMemo(memo)
    }
}

class Holder(val binding: ItemRecyclerBinding) : RecyclerView.ViewHolder(binding.root) {
    fun setMemo(memo : Memo){
        binding.textNo.text = "${memo.no}"
        binding.textTitle.text=memo.title

        var sdf =SimpleDateFormat("yyyy/MM/dd")
        var formattedDate = sdf.format(memo.timestamp)
        binding.textDate.text=formattedDate
    }
}
```
<img width="172" alt="git_3" src="https://user-images.githubusercontent.com/80842764/116982862-50ae3280-ad04-11eb-855a-73b292e4591d.PNG">

#### 레이아웃 매니저의 종류
* LinearLayoutManager
```kotlin
///세로스크롤
LinearLayoutManager(this)

///가로스크롤
LinearLayoutManager(this, LinearLayoutManager.HORIZONTAL, false) //두번째 파라미터: 가로 스크롤 옵션 설정
```
* GridLayoutManager
```kotlin
GridLayoutManager(this, 3) // ->한 줄에 3개의 아이템을 표시
```
* StaggeredGridLayoutManager
```kotlin
///세로스크롤
StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.VERTICAL)  // ->한 줄에 3개의 아이템을 표시

///가로스크롤
StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.HORIZONTAL)
```

#### 목록 클릭 이벤트 처리

> CustomAdapter.kt의 class Holder에 추가
```kotlin
init {
        binding.root.setOnClickListener{
            Toast.makeText(binding.root.context, "클릭된 아이템 = ${binding.textTitle.text}", Toast.LENGTH_LONG).show()
        }
}
    
```
