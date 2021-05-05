# Activity
: 사용자가 직접 보고 입력하는 화면을 담당하는 컴포넌트

- [Intent](https://github.com/jimin3263/kotlin_study/blob/main/Jimin/week_4.md#intent)
- [Spinner](https://github.com/jimin3263/kotlin_study/blob/main/Jimin/week_4.md#%EC%8A%A4%ED%94%BC%EB%84%88)
- [RecyclerView](https://github.com/jimin3263/kotlin_study/blob/main/Jimin/week_4.md#%EB%A6%AC%EC%82%AC%EC%9D%B4%ED%81%B4%EB%9F%AC%EB%B7%B0)
- [Fragment](https://github.com/jimin3263/kotlin_study/blob/main/Jimin/week_4.md#fragment)

## Context
- 시스템을 사용하기 위한 정보와 도구가 담겨 있는 클래스
- 대부분 context는 컴포넌트 실행시 함께 생성, 생성된 컴포넌트가 가지고 있는 메서드를 호출해 각각의 도구 사용할 수 있음
- Application Context
  - 애플리케이션과 관련된 핵심 기능 담고 있는 클래스
  - 하나의 인스턴스만 생성됨
  - 호출하는 지점과 관계없이 동일한 컨텍스트 호출됨
- Base Context
  - 4대 컴포넌트 -> activity, service, content provider, broadcast receiver의 기반 클래스
  - 컴포넌트 개수만큼 컨텍스트 함께 생성 -> 호출되는 지점에 따라 다른 컨텍스트 호출

## Intent

- 실행할 대상의 액티비티 이름과 전달할 데이터를 담아서 인텐트 생성
- 생성한 인텐트를 startActivity() 메서드에 담아서 호출 -> 액티비티 매니저에 전달
- 액티비티 매니저는 인텐트 분석해, 지정한 액티비티를 실행시킴
- 전달된 인텐트 -> 타깃 액티비티에 전달
- 타깃 액티비티에서는 전달받은 인텐트에 데이터가 있다면 이를 꺼내서 사용

### Main activity에서 Sub activity 실행

> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent = Intent(this, SubActivity::class.java)
        binding.button.setOnClickListener{ startActivity(intent)}

    }
}
```

### 액티비티 사이 값 주고 받기

> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent = Intent(this, SubActivity::class.java)
        // 키, 값 조합으로 번들에 직접 넣음, 꺼낼 때는 키 이용해서 꺼냄
        intent.putExtra("from1","hello bundle")
        intent.putExtra("from2", 2021)
        binding.button.setOnClickListener{ startActivity(intent)}

    }
}
```
> SubActivity.kt
```kotlin
class SubActivity : AppCompatActivity() {

    val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)
        
        // intent 이용, key를 통해서 값 받음
        binding.to1.text = intent.getStringExtra("from1")
        // text는 문자열만 받을 수 있기 때문에 "" 감싸고 문자열 템플릿을 사용해서 문자열로 변환
        binding.to2.text = "${intent.getIntExtra("from2",0)}"
    }
}
```

### 메인 액티비티에서 값 돌려받기
> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent = Intent(this, SubActivity::class.java)
        intent.putExtra("from1","hello bundle")
        intent.putExtra("from2", 2021)
        
        //값 돌려받기 위해서 startActivityForResult(Intent, requestCode) 사용 
        binding.button.setOnClickListener{ startActivityForResult(intent,99)}
    }
    
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (resultCode == Activity.RESULT_OK){
            when(requestCode) {
                99 -> {
                    val message = data?.getStringExtra("returnValue")
                    Toast.makeText(this, message, Toast.LENGTH_LONG).show()
                }
            }
        }
    }
}
```

> SubActivity.kt
```kotlin
class SubActivity : AppCompatActivity() {

    val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        binding.to1.text = intent.getStringExtra("from1")
        binding.to2.text = "${intent.getIntExtra("from2",0)}"


        binding.button2.setOnClickListener{
            val returnIntent = Intent()
            //입력된 문자열 intent에 put
            returnIntent.putExtra("returnValue",binding.editText.text.toString())
            
            //setResult(상태값, 인텐트)
            setResult(Activity.RESULT_OK,returnIntent)
            finish()
        }
    }
}
```

## 생명 주기

|메서드|액티비티 상태|설명|
|------|---|---|
|OnCreate()|만들어짐|액티비티 실행됨|
|OnStart()|화면에 나타남|화면에 보이기 시작|
|OnResume()|현재 실행 중|실제 액티비티가 실행 중|
|OnPause()|화면 가려짐|액티비티 일부가 다른 액티비티에 가려짐|
|OnStop()|화면 없어짐|다른 액티비티가 실행되어서 화면이 완전히 가려짐|
|OnDestroy()|종료됨|액티비티가 종료됨|

## 스피너
: 내부적으로 복수의 데이터 처리 가능

<img src = "https://user-images.githubusercontent.com/50178026/117013104-85cd7b80-ad2a-11eb-9d03-b5893398a716.png" height="550" width="300">

> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        var data = listOf("-선택-","1월","2월","3월","4월","5월","6월")
        //ArrayAdapter<>(스피너를 화면에 그리기 위한 컨텍스트, 스피너에 보여줄 목록이 그려질 레이아웃, 어댑터에서 사용할 데이터)
        var adapter = ArrayAdapter<String>(this,android.R.layout.simple_list_item_1,data)
        binding.spinner.adapter = adapter

        binding.spinner.onItemSelectedListener = object: AdapterView.OnItemSelectedListener{
            override fun onNothingSelected(parent: AdapterView<*>?) {
            }

            override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
                binding.result.text=data.get(position)
            }
        }

    }
}
```

## 리사이클러뷰

<img src="https://user-images.githubusercontent.com/50178026/117020013-f9728700-ad30-11eb-97c2-1db3868be5c7.png" height="550" width="300">

> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        fun loadData(): MutableList<Memo>{
            val data:MutableList<Memo> = mutableListOf()
            for (no in 1..50){
                val title = "이것이 코틀린 안드로이드다 ${no+1}"
                val date = System.currentTimeMillis()
                var memo = Memo(no,title,date)
                data.add(memo)
            }
            return data;
        }

        //data 입력
        val data:MutableList<Memo> = loadData()

        //data adapter에 넣음
        var adapter= CustomAdapter()
        adapter.listData = data

        binding.recyclerView.adapter= adapter
        binding.recyclerView.layoutManager = LinearLayoutManager(this)

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
        binding.textView.text = "${memo.no}"
        binding.textView2.text=memo.title
        // 형식 지정  
        var sdf = SimpleDateFormat("yyyy/MM/dd")
        var formattedDate = sdf.format(memo.timestamp)
        binding.textView3.text=formattedDate
    }
}
```

> Memo.kt
```kotlin
data class Memo (var no: Int, var title:String, var timestamp: Long )
```


### 클릭 시 처리
> CustomAdapter.kt
```kotlin
class Holder(val binding: ItemRecyclerBinding) : RecyclerView.ViewHolder(binding.root) {
    /*
    
    */
    
    init{
        binding.root.setOnClickListener{
            Toast.makeText(binding.root.context, "클릭된 아이템 = ${binding.textView2.text}", Toast.LENGTH_LONG).show()
        }
    }
}
```

### Layout Manager
- LinearLayoutManager
  - 세로: LinearLayoutManager(this)
  - 가로: LinearLayoutManager(this, LinearLayoutManager.HORIZONTAL, false)
- GridLayoutManager
  - GridLayoutManager(this, 한 줄에 표시할 아이템 개수)
- StaggeredGridLayoutManager
  - 세로 스크롤: StaggeredGridLayoutManager(한 줄에 표시할 아이템 개수, StaggeredGridLayoutManager.VERTICAL)
  - 가로 스크롤: StaggeredGridLayoutManager(한 줄에 표시할 아이템 개수, StaggeredGridLayoutManager.HORIZONTAL)


## Fragment

### 액티비티에 fragment 추가하기

<img src="https://user-images.githubusercontent.com/50178026/117165546-8df7ea80-ae00-11eb-956f-2736c515052a.png" height="550" width="300">
                                                                                                                                     
> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)
        setFragmnet()
    }

    fun setFragmnet(){
        val listFragment: ListFragment = ListFragment()
        // begin transaction
        val transaction= supportFragmentManager.beginTransaction()
        // add fragment
        transaction.add(R.id.FrameLayout,listFragment)
        // commit transaction
        transaction.commit()
    }
}
```

### xml에서 프래그먼트 추가

<img src="https://user-images.githubusercontent.com/50178026/117167764-820d2800-ae02-11eb-8a2f-5f575eecb3b3.png" height="550" width="300">

- 이전과 같은 화면을 확인할 수 있다
- 화면 전환이 없을 때 이 방법이 더 효율적!

> activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/Activity_text"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:layout_marginTop="16dp"
        android:text="Activity"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <fragment
        android:id="@+id/fragment"
        android:name="com.example.fragment.ListFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="50dp"
        app:layout_constraintTop_toBottomOf="@+id/Activity_text"
        tools:layout_editor_absoluteX="165dp"
        tools:layout_editor_absoluteY="50dp" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

### 프래그먼트 전환

<img src="https://user-images.githubusercontent.com/50178026/117173143-6f492200-ae07-11eb-825e-9b26ce10eea2.png" height="550" width="300"> <img src="https://user-images.githubusercontent.com/50178026/117173177-7839f380-ae07-11eb-9d9a-de9af0c83b00.png" height="550" width="300">

> MainActivity.kt
 ```kotlin
 class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        setFragmnet()

    }

    //Next 클릭 -> detailFragment
    fun goDetail(){
        val detailFragment = DetailFragment()

        val transaction= supportFragmentManager.beginTransaction()
        transaction.add(R.id.FrameLayout,detailFragment)
        //뒤로가기 허
        transaction.addToBackStack("detail")
        transaction.commit()
    }
    //뒤로가기 클릭 -> ListFragment
    fun goBack(){
        onBackPressed()
    }

    fun setFragmnet(){
        val listFragment: ListFragment = ListFragment()
        // begin transaction
        val transaction= supportFragmentManager.beginTransaction()
        // add fragment
        transaction.add(R.id.FrameLayout,listFragment)
        // commit transaction
        transaction.commit()
    }

}
 ```
> DetailFragment.kt
```kotlin
class DetailFragment : Fragment() {
    var mainActivity: MainActivity? =null

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val binding = FragmentDetailBinding.inflate(inflater,container,false)
        binding.button.setOnClickListener{mainActivity?.goBack()}

        return binding.root

    }

    override fun onAttach(context: Context) {
        super.onAttach(context)

        // context 캐스팅 -> MainActivity에 담음
        mainActivity = context as MainActivity
    }

}
```
> ListFragment.kt
```kotlin
class ListFragment : Fragment() {
    var mainActivity: MainActivity? = null

    // 리사이클러의 onCreateViewHolder() 메서드와 유사
    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        //inflater로 생성한 뷰 담아두고, binding해온 view내에 버튼에 리스터 등록
       val binding = FragmentListBinding.inflate(inflater,container,false)
        binding.button.setOnClickListener{mainActivity?.goDetail()}

        return binding.root
    }

    override fun onAttach(context: Context) {
        super.onAttach(context)

        // context 캐스팅 -> MainActivity에 담음
        mainActivity = context as MainActivity
    }
}
```

- 겹치기 때문에 Background color 설정해줘야 함 


### 프래그먼트로 값 전달

<img src ="https://user-images.githubusercontent.com/50178026/117175608-fe573980-ae09-11eb-8fda-88d189414fd7.png" width = "300" height = "550">

> MainActivity.kt
```kotlin
 fun setFragmnet(){
        val listFragment: ListFragment = ListFragment()

        var bundle = Bundle()
        bundle.putString("k1","안녕")
        
        
        listFragment.arguments = bundle
        // begin transaction
        val transaction= supportFragmentManager.beginTransaction()
        // add fragment
        transaction.add(R.id.FrameLayout,listFragment)
        // commit transaction
        transaction.commit()
    }
```

> ListFragmnet.kt
```kotlin
verride fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {

       val binding = FragmentListBinding.inflate(inflater,container,false)
        binding.button.setOnClickListener{mainActivity?.goDetail()}

        val title = arguments?.getString("k1")

        binding.textView.text= title

        return binding.root
    }
```

### 프래그먼트의 생명주기

#### 생성 주기
- onAttach()
  - commit 되는 순간 호출
  - 파라미터로 전달되는 context를 저장해 놓고 사용하거나 context로부터 상위 액티비티 꺼내서 사용
- onCreate()
  - 프래그먼트 생성될 때 호출
  - 변수 초기화할 때 사용
- onCreateView()
  - 사용자 인터페이스 관련된 뷰 초기화
- onStart()
  - 화면에서 사라졌다가 다시 나타날 때 호출
  - 화면 생성 후, 화면에 입력될 값 초기화하는 용도
- onResume()
  - onPause() 상태에서 멈추고 바로 호출

#### 소멸 주기
- onPause()
  - 프래그먼트가 화면에서 사라지면 호출
  - 일시정지
- onStop()
  - 프래그먼트가 일부분이라도 보이면 onStop()은 호출 안함
  - 정지
- onDestroyView()
  - 뷰의 초기화 해제
  - onCreateView()에서 생성한 View 모두 소멸
- onDestroy
  - 액티비티에는 남아있지만 프래그먼트 자체는 소멸
  - 모든 자원 해제
- onDetach()
  - 액티비티에서 연결 해제
