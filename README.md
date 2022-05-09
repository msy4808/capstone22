팀명 : 스테로이드

이름 : 문성운 (팀장: App 기능개발)

졸업작품 소개 사이트 : URL 추가예정

포트폴리오 소개 사이트 : URL 추가예정

# [졸업작품 소개]

-작품명 :  smartrip

-개발환경 : Android Studio - Kotlin

-작품 소개 : 해외여행시 사용하는 도우미 앱

-작품의 특징 : 번역, 날씨 등등 해외여행에서 기초적으로 필요한 것들을 지원해줌

# **[개발일지]**

- **※**
    
    -최소한 일주일에 한번(강의가 있는 날짜로 작성)
    
    (내용은 자유, 회의내용, 개발경과, 오류해결, 보고서 작성(제출))
    
    
## 5월 4일

### 메인 페이지 디자인 적용 및 앱 구조변경

- 기존에 MainActivity 하나만 쓰는 구조에서 각 화면별로 프래그먼트로 변경

- HomeFragment.kt (카메라와 날씨탭은 추가예정)

```kotlin
package com.steroid.travel_roid

import android.os.Bundle
import android.os.Handler
import android.os.Looper
import android.os.Message
import android.text.Editable
import android.text.TextWatcher
import androidx.fragment.app.Fragment
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.*
import java.util.*

class HomeFragment : Fragment() {
    var langCode = ""
    var autoLangCode = ""
    var response_Text = ""
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val view = inflater.inflate(R.layout.fragment_home, container, false)
        val userEnterText: EditText = view.findViewById(R.id.textIn)
        val result: TextView = view.findViewById(R.id.result)
        val outSpinner: Spinner = view.findViewById(R.id.langTag) //spinner 메뉴
        val targetSpinner: Spinner = view.findViewById(R.id.langTag2)

        val handler = object:Handler(Looper.getMainLooper()){ //감지된 언어코드로 Spinner를 변경해주기 위해 핸들러 사용
            override fun handleMessage(msg: Message) {
                when (msg.what) {
                    0 -> {
                        outSpinner.setSelection(0)
                    }
                    1 -> {
                        outSpinner.setSelection(1)
                    }
                    2 -> {
                        outSpinner.setSelection(2)
                    }
                    3 -> {
                        outSpinner.setSelection(3)
                    }
                    4 -> {
                        outSpinner.setSelection(4)
                    }
                    5 -> {
                        outSpinner.setSelection(5)
                    }
                    6 -> {
                        outSpinner.setSelection(6)
                    }
                    7 -> {
                        outSpinner.setSelection(7)
                    }
                    8 -> {
                        outSpinner.setSelection(8)
                    }
                    9 -> {
                        outSpinner.setSelection(9)
                    }
                    10 -> {
                        outSpinner.setSelection(10)
                    }
                    11 -> {
                        outSpinner.setSelection(11)
                    }

                    12 -> {
                        outSpinner.setSelection(12)
                    }
                    13 -> {
                        outSpinner.setSelection(13)
                    }
                    14 -> {
                        outSpinner.setSelection(14)
                    }
                    15 -> {
                        outSpinner.setSelection(15)
                    }
                    16 -> {
                        outSpinner.setSelection(16)
                    }
                    17 -> {
                        outSpinner.setSelection(17)
                    }
                    99 -> {
                        result.text = response_Text
                    }
                }
            }
        }


        //spinner 메뉴 어댑터 연결
        outSpinner.adapter = ArrayAdapter.createFromResource(requireContext(), R.array.langList, android.R.layout.simple_spinner_item)
        targetSpinner.adapter = ArrayAdapter.createFromResource(requireContext(), R.array.target_langList, android.R.layout.simple_spinner_item)

        //spinner 리스너 설정
        outSpinner.onItemSelectedListener = object: AdapterView.OnItemSelectedListener {
            override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) { //감지가 아니라 직접 선택해도 전달되게 ... 우선 만들어놈
                when(position) {
                    0 -> {
                        autoLangCode = "ko"
                    }
                    1 -> {
                        autoLangCode = "ja"
                    }
                    2 -> {
                        autoLangCode = "zh-CN"
                    }
                    3 -> {
                        autoLangCode = "zh-TW"
                    }
                    4 -> {
                        autoLangCode = "hi"
                    }
                    5 -> {
                        autoLangCode = "en"
                    }
                    6 -> {
                        autoLangCode = "es"
                    }
                    7 -> {
                        autoLangCode = "fr"
                    }
                    8 -> {
                        autoLangCode = "de"
                    }
                    9 -> {
                        autoLangCode = "pt"
                    }
                    10 -> {
                        autoLangCode = "vi"
                    }
                    11 -> {
                        autoLangCode = "id"
                    }
                    12 -> {
                        autoLangCode = "fa"
                    }
                    13 -> {
                        autoLangCode = "ar"
                    }
                    14 -> {
                        autoLangCode = "mm"
                    }
                    15 -> {
                        autoLangCode = "th"
                    }
                    16 -> {
                        autoLangCode = "ru"
                    }
                    17 -> {
                        autoLangCode = "it"
                    }

                }
            }

            override fun onNothingSelected(p0: AdapterView<*>?) {
            }
        }

        targetSpinner.onItemSelectedListener = object: AdapterView.OnItemSelectedListener {
            //Spinner에서 선택한 target 언어코드를 langCode에 저장하는 코드
            override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
                when(position) {
                    0 -> {
                        langCode = "ko"
                    }
                    1 -> {
                        langCode = "en"
                    }
                    2 -> {
                        langCode = "ja"
                    }
                    3 -> {
                        langCode = "zh-TW"
                    }
                    4 -> {
                        langCode = "zh-CN"
                    }
                    5 -> {

                        langCode = "vi"
                    }
                    6 -> {
                        langCode = "id"
                    }
                    7 -> {
                        langCode = "th"
                    }
                    8 -> {
                        langCode = "de"
                    }
                    9 -> {
                        langCode = "es"
                    }
                    10 -> {
                        langCode = "fr"
                    }
                    11 -> {
                        langCode = "ru"
                    }
                    12 -> {
                        langCode = "it"
                    }

                }
            }

            override fun onNothingSelected(p0: AdapterView<*>?) {
            }
        }

        val textWatcher = object: TextWatcher{
            override fun beforeTextChanged(p0: CharSequence?, p1: Int, p2: Int, p3: Int) {
            }

            override fun onTextChanged(p0: CharSequence?, p1: Int, p2: Int, p3: Int) {
            }

            override fun afterTextChanged(p0: Editable?) { //텍스트가 입력되면 동작함 <- 입력된 텍스트를 String으로 받아 DetectLangs클래스로 넘겨줌
                val timer = Timer()
                timer.schedule(object: TimerTask(){
                    override fun run() {
                        val detectLangs = DetectLangs(p0.toString())
                        autoLangCode = detectLangs.getlangCode()
                        when(autoLangCode){ //감지된 언어코드에 따라 핸들러에 msg로 넘겨줌
                            "ko" -> {
                                handler.sendEmptyMessage(0)
                            }
                            "ja" -> {
                                handler.sendEmptyMessage(1)
                            }
                            "zh-CN" -> {
                                handler.sendEmptyMessage(2)
                            }
                            "zh-TW" -> {
                                handler.sendEmptyMessage(3)
                            }
                            "hi" -> {
                                handler.sendEmptyMessage(4)
                            }
                            "en" -> {
                                handler.sendEmptyMessage(5)
                            }
                            "es" -> {
                                handler.sendEmptyMessage(6)
                            }
                            "fr" -> {
                                handler.sendEmptyMessage(7)
                            }
                            "de" -> {
                                handler.sendEmptyMessage(8)
                            }
                            "pt" -> {
                                handler.sendEmptyMessage(9)
                            }
                            "vi" -> {
                                handler.sendEmptyMessage(10)
                            }
                            "id" -> {
                                handler.sendEmptyMessage(11)
                            }
                            "fa" -> {
                                handler.sendEmptyMessage(12)
                            }
                            "ar" -> {
                                handler.sendEmptyMessage(13)
                            }
                            "mm" -> {
                                handler.sendEmptyMessage(14)
                            }
                            "th" -> {
                                handler.sendEmptyMessage(15)
                            }
                            "ru" -> {
                                handler.sendEmptyMessage(16)
                            }
                            "it" -> {
                                handler.sendEmptyMessage(17)
                            }
                        }
                        val translate = TranslateTask(userEnterText.text.toString(), autoLangCode, langCode) //텍스트와 두가지의 언어코드를 파라미터로 보냄
                        response_Text = translate.execute().get()
                        handler.sendEmptyMessage(99)
                    }
                },1000)
            }
        }

        userEnterText.addTextChangedListener(textWatcher) //editText에텍스트가 입력되면 동작하는 리스너를 연결
        return view
    }
}
```

---

## 4월 18일

### 현재 카카오 로그인 API 토큰 받아오는 부분에서 넘어가지않는 에러 발생

- 해당 에러 해결 - 매니페스트 파일 수정

```xml
<activity
            android:name="com.kakao.sdk.auth.AuthCodeHandlerActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />

                <data android:host="oauth"
                    android:scheme="kakaod3bc84d744e74ec2f19755c8cc701ad5" />
            </intent-filter>
        </activity>
```

---

## 4월 13일

### 현재 카카오 로그인 API 토큰 받아오는 부분에서 넘어가지않는 에러 발생

- 로그 찍으며 디버깅 예정 - 에러수정이 안될시 로그인API를 네이버로 변경해서 재시도

### 번역 클래스 코드 - TranslateTask.kt

```kotlin
package com.steroid.travel_roid

import android.os.AsyncTask
import android.util.Log
import com.google.gson.JsonElement
import com.google.gson.JsonParser
import java.io.*
import java.lang.RuntimeException
import java.net.HttpURLConnection
import java.net.MalformedURLException
import java.net.URL
import java.net.URLEncoder

valclientId= "Ge3xCYIlR7pE8p7yNiVe"
valclientSercret= "cP885YoL58"

fun connect(apiURL: String): HttpURLConnection {
    return try {
        val url = URL(apiURL)
        (url.openConnection() as HttpURLConnection)
    }catch (e: MalformedURLException){
        throw RuntimeException("API URL 오류", e)
    }catch (e: IOException) {
        throw RuntimeException("연결 실패",e)
    }
}

class TranslateTask(translationText:String, langCode: String, targetLangCode: String) : AsyncTask<String, Void, String> (){
    var langCode = langCode
    var targetLangCode = targetLangCode
    var translationText = translationText
    override fun doInBackground(vararg p0: String?): String {
        val apiURL = "https://openapi.naver.com/v1/papago/n2mt"
        var text: String = translationText
        text = try {
            URLEncoder.encode(translationText, "UTF-8")
        }catch (e: UnsupportedEncodingException) {
            throw RuntimeException("인코딩 실패", e)
        }
        val requestHeaders: MutableMap<String, String> = HashMap()
        requestHeaders["X-Naver-Client-Id"] =clientId
requestHeaders["X-Naver-Client-Secret"] =clientSercret

fun readBody(body: InputStream): String {
            val streamReader = InputStreamReader(body);
            try{
                BufferedReader(streamReader).use{lineReader->
val responseBody = StringBuilder()
                    var line: String?
                    while (lineReader.readLine().also{line =it }!= null) {
                        responseBody.append(line)
                    }
                    return responseBody.toString()
}
}catch (e: IOException){
                throw RuntimeException("API 응답 리드 실패", e)
            }
        }

        fun post(apiUrl: String, requestHeaders: Map<String, String>, text: String): String {
            val con: HttpURLConnection =connect(apiUrl)
            val postParams = "source=$langCode&target=$targetLangCode&text=$text"
println("번역 코드 테스트 ; $postParams")
            try{
                con.requestMethod= "POST"

                for (header: Map.Entry<String, String> in requestHeaders.entries){
                    con.setRequestProperty(header.key, header.value)
                }
                con.doOutput= true
                DataOutputStream(con.outputStream).use{wr->
wr.write(postParams.toByteArray())
                    wr.flush()
}
val responseCode = con.responseCode
if(responseCode == HttpURLConnection.HTTP_OK) {
                    return readBody(con.inputStream)
                }else{
                    return readBody(con.errorStream)
                }
            }catch (e: IOException){
                throw RuntimeException("API 요청과 응답 실패", e)
            } finally {
                con.disconnect()
            }
        }

        val responseBody: String = post(apiURL, requestHeaders, text)
println("번역결과 : $responseBody")

        var parser: JsonParser = JsonParser()
        var element: JsonElement = parser.parse(responseBody)
        var data: String = ""

        if(element.asJsonObject.get("errorMessage") != null){
            Log.d("번역오류", "번역오류 발생 : ${element.asJsonObject.get("errorCode").toString()}")
            data = "A: 오류"
        }else if (element.asJsonObject.get("message") != null){
            data = element.asJsonObject.get("message").getAsJsonObject().get("result").asJsonObject.get("translatedText").asString

Log.d("번역성공", "성공 : $data")
        }
        return data
    }
}
```

---

## 4월 10일 ~ 11일

### API 테스트(현재 디자인이 아직이므로 테스트 후 디자인 나오면 기능삽입예정)

- 파파고 언어감지 API 적용
- 번역 API 수정 (번역할 언어 18종 추가)

---

## 4월 06일

### API 테스트(현재 디자인이 아직이므로 테스트 후 디자인 나오면 기능삽입예정)

- 파파고 번역 API 테스트(성공) - 현재 한국어에서 영어만 가능
- 파파고 언어감지 API 테스트 예제 코드분석

---

## 3월 30일

### 개발환경 구성

- Git 설치 및 Repo 구성원 추가
- 파파고 API Key 발급

---

## 3월 23일

### 앱기능

- 기본 텍스트 번역
- 음성번역
- 사진찍어서 텍스트 번역
- 내 현재위치 날씨 + 내 위치랑 지정된 위치(한국) 시차

## API 찾기

- 번역API
- 텍스트 추출 API
- GPS 좌표 API(Geocoder로 가능한지..?)
- Geocoder( 코틀린에서 지원)
- 날씨 API, DB
- 로그인 API( 네이버, 카카오톡 등등...)
- 필요한 기능 있으면 추가예정 ...
- 디자인 API(메테리얼 디자인등등 이쁜거) 기본 안드로이드 디자인 X
