# [Model-View-ViewModel (ie MVVM)](https://github.com/ahmedeltaher/Android-MVVM-architecture)



[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-android--best--practices-brightgreen.svg?style=flat)](https://android-arsenal.com/details/3/4975)  [![kotlin](https://img.shields.io/badge/Kotlin-1.3.xxx-brightgreen.svg)](https://kotlinlang.org/)  [![coroutines](https://img.shields.io/badge/coroutines-asynchronous-red.svg)](https://kotlinlang.org/docs/reference/coroutines-overview.html) [![ANKO](https://img.shields.io/badge/Anko-commons-blue.svg)](https://github.com/Kotlin/anko) [![Mockk](https://img.shields.io/badge/Mockk-testing-yellow.svg)](https://mockk.io/)      [![Junit5](https://img.shields.io/badge/Junit5-testing-yellowgreen.svg)](https://junit.org/junit5/)   [![Espresso](https://img.shields.io/badge/Espresso-testing-lightgrey.svg)](https://developer.android.com/training/testing/espresso/)  [![Dagger 2](https://img.shields.io/badge/Dagger-2.xx-orange.svg)](https://google.github.io/dagger/)  [![Kotlin-Android-Extensions ](https://img.shields.io/badge/Kotlin--Android--Extensions-plugin-red.svg)](https://kotlinlang.org/docs/tutorials/android-plugin.html) [![MVVM ](https://img.shields.io/badge/Clean--Code-MVVM-brightgreen.svg)](https://github.com/googlesamples/android-architecture)  ![MVP ](https://img.shields.io/badge/Clean--Code-MVP-brightgreen.svg)  
  
![MVVM3](https://user-images.githubusercontent.com/1812129/68319232-446cf900-00be-11ea-92cf-cad817b2af2c.png)

Model-View-ViewModel (ie MVVM) is a template of a client application architecture, proposed by John Gossman as an alternative to MVC and MVP patterns when using Data Binding technology. Its concept is to separate data presentation logic from business logic by moving it into particular class for a clear distinction.  
You can also check [**MVP**](https://github.com/ahmedeltaher/Android-MVP-Architecture) 
  
  
**What is Coroutines ?**  
-------------------  
  
 **Coroutines :**  
Is light wight threads for asynchronous programming, Coroutines not only open the doors to  
asynchronous programming, but also provide a wealth of other possibilities such as concurrency, actors, etc.  
  
----------  
  
**Coroutines VS RXJava**  
-------------------  
They're different tools with different strengths. Like a tank and a cannon, they have a lot of overlap but are more or less desirable under different circumstances.  
        - Coroutines Is light wight threads for asynchronous programming.  
        - RX-Kotlin/RX-Java is functional reactive programming, its core pattern relay on  
        observer design pattern, so you can use it to handle user interaction with UI while you  
        still using coroutines as main core for background work.  
  
**How does Coroutines concept work ?**  
------------  
 - Kotlin coroutine is a way of doing things asynchronously in a sequential manner. Creating a coroutine is a lot cheaper vs creating a thread.  
  
  
**When I can choose Coroutines or RX-Kotlin to do some behaviour ?**  
--------------------------  
 - Coroutines : *When we have concurrent tasks , like you would fetch data from Remote connections  
 , database , any background processes , sure you can use RX in such cases too, but it looks like  
  you use a tank to kill ant.*  
 - RX-Kotlin : *When you would to handle stream of UI actions like : user scrolling , clicks ,  
 update UI upon some events .....ect .*  
  
  
**What is the Coroutines benefits?**  
-----------------------------  
  
 - Writing an asynchronous code is sequential manner.  
 - Costing of create coroutines are much cheaper to crate threads.  
 - Don't be over engineered to use observable pattern, when no need to use it.  
 - parent coroutine can automatically manage the life cycle of its child coroutines for you.  
  
  
**Handle Retrofit with Coroutines**  
-----------------------------  
  
![8399](https://user-images.githubusercontent.com/1812129/68318999-e93b0680-00bd-11ea-9d76-058222c7a654.png)  
  
 - Add Coroutines to your gradle file  
  
>     // Add Coroutines  
>     implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.2'  
>     implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.2'  
>     implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core-common:1.3.2'  
>     // Add Retrofit2  
>     implementation 'com.squareup.retrofit2:retrofit:2.6.2'  
>     implementation 'com.squareup.retrofit2:converter-gson:2.6.2'  
>     implementation 'com.squareup.okhttp3:okhttp:4.2.2'  
  
  
 - Make Retrofit Calls.  
  
>     @GET("topstories/v2/home.json")  
>     fun fetchNews(): Call<NewsModel>  
  
  
 - With ```async``` we create new coroutine and returns its future result as an implementation of [Deferred].  
 - The coroutine builder called ```launch``` allow us to start a coroutine in background and keep working in the meantime.  
 - so async will run in background then return its promised result to parent coroutine which  
 created by launch.  
 - when we get a result, it is up to us to do handle the result. 
  
  
  
  
  
>     launch {  
>       try {  
>             val serviceResponse: Data? = withContext(Dispatchers.IO) { dataRepository.requestNews()  
>            }  
>       if (serviceResponse?.code == Error.SUCCESS_CODE) {  
>                 val data = serviceResponse.data  
>                 callback.onSuccess(data as NewsModel)  
>             } else {  
>                 callback.onFail(serviceResponse?.error)  
>             }  
>         } catch (e: Exception) {  
>                 callback.onFail(Error(e))  
>         }  
>     }  
  
  
  
  
  
**Keep your code clean according to MVVM**  
-----------------------------  
 - Yes , liveData is easy , powerful , but you should know how to use.  
 - For livedate which will emit data stream , it has to be in your  
   data layer , and don't inform those observables any thing else like  
   in which thread those will consume , cause it is another  
 - For livedata which will emit UI binding events, it has to be in your ViewModel Layer.  
 - Observers in UI Consume and react to live data values and bind it.  
   responsibility , and according to `Single responsibility principle`  
  in `SOLID (object-oriented design)` , so don't break this concept by  
   mixing the responsibilities .  
    
  ![mvvm2](https://user-images.githubusercontent.com/1812129/68319008-e9d39d00-00bd-11ea-9245-ebedd2a2c067.png)

## LICENSE
Copyright [2016] [Ahmed Eltaher]    
Licensed under the Apache License, Version 2.0 (the "License");    
you may not use this file except in compliance with the License.    
You may obtain a copy of the License at    
    
 http://www.apache.org/licenses/LICENSE-2.0    
Unless required by applicable law or agreed to in writing, software    
distributed under the License is distributed on an "AS IS" BASIS,    
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.    
See the License for the specific language governing permissions and    
limitations under the License.