# MVC, MVP, MVVM 디자인 패턴

MVVM을 이해하기 위해서는

MVC -> MVP -> MVVM 순서대로 아키텍처 패턴에 대한 이해가 필요하다.

##  

## MVC 패턴

객체지향프로그래밍에서 MVC란 사용자 인터페이스를 성공적이며 효과적으로 데이터 모형에 관련 시키기 위한 방법론 또는 설계 방식중 하나로써, 목적 코드의 재사용에 유용한 것은 물론, 사용자 인터페이스와 응용프로그램 개발에 소요되는 시간을 현저하게 줄여주는 형식이라고 많은 개발자들이 평가하고 있다.

 

Model, View, Controller의 약자로 User – View – Controller – Model – Controller – View User의 구조를 가지고 있다.

 

MVC 패턴은 응용프로그램의 시각적 부분과 가 이면의 동작과 제어를 처리하는 부분(비즈니스 로직이라 한다)을 분리하여 서로에 미치는 영향 없이도 응용프로그램을 변경할 수 있다는 장점이 있다.

 

예를 들어 데이터베이스나 제어프로그램의 변경 없이 시각적인 부분만 수정하려면 view에 해당하는 부분만 수정하면 되고 시각적인 부분과 관계 없이 데이터 처리 부분만 수정하려면 model 부분만, 프로그램간 연결과 제어를 수정하려면 controller 부분만 수정하면 되는 방식이다.

 

Model과 View는 뒤에 나올 MVP와 MVVM에 계속해서 등장할 것이므로 확실하게 알아두자.



![img](https://blog.kakaocdn.net/dn/S2B7s/btsl1gbcAqf/qiuQMQMwjkM8g0tXylwvG0/img.png)



### **MVC 패턴의 구조**

#### **M (Model)**

> 데이터를 처리하는 역할

 

애플리케이션의 정보(데이터)를 처리하는 컴포넌트를 말한다. 다시 말해 데이터베이스에 연결하고 데이터를 추출하거나 저장, 삭제, 업데이트, 변환 등의 작업을 수행하는 역할을 한다.

####  

#### **V (View)**

> 사용자가 보는 화면

 

View는 말그대로 화면에 표시되는 부분이다. 추출한 데이터나 일반적인 텍스트 데이터를 표시하거나 input, button등의 사용자 인터페이스 요소, 데이터 및 객체의 입력, 출력 또는 사용자와의 상호작용을 위한 인터페이스를 표시하는 영역이다. 담당하는 사용자가 볼 수 있는 화면이다.

####  

#### **C (Controller)**

> 데이터와 뷰를 연결, 제어하는 역할
> 사용자의 입력(Action)을 받고 처리하는 부분

 

Controller는 어플리케이션에서 각 요소들의 연결관계를 설정하고 데이터와 시각적 부분의 연결 등을 관리한다. 대개 url로부터 입력되는 정보로부터 어떤 데이터와 뷰를 연결할 지 등을 제어한다.

사용자가 Controller에 작업을 요청하면 Controller는 Model을 호출하여 데이터를 처리하고 Model이 데이터를 처리한 결과를 View에 보내고 이 결과를 사용자가 보게 된다는 것이다.

Model과 View를 이어주는 다리 역할, 모든 “이벤트”를 처리하는 부분, 메인 로직을 담당. Model과 View를 연결하고 있는 클래스를 대표, Model과 View 내의 클래스들 간 정보 교환하는데 사용한다.

###  

### **MVC패턴 사용 목적**

View와 Model사이에 Controller를 두어 View와 Model의 의존성을 없애기 위해서 사용한다.

###  

### **MVC패턴** **동작 방법**



![img](https://blog.kakaocdn.net/dn/Vgj1v/btsl2R2tmL5/v0VLPEO7f2kX4O9JCmFuWk/img.png)



 

1. 사용자의 Action들은 Controller가 감지 한다. 
2. Controller는 사용자의 Action을 확인하고, Model을 업데이트 한다.
3. Controller는 Model을 표현해줄 View를 선택한다. 
4. View는 Model을 이용하여 화면을 나타낸다. 

###  

### **MVC 패턴의 특징**

- 사용자 Action이 Controller로 들어오며, 모델에서 처리한 데이터를 뷰로 직접 넘겨준다.
- Controller와 뷰와의 관계가 1:n이다.

###  

### **MVC패턴의 장점**

- 전형적인 어플리케이션 OOP 구조로써 가장 단순하며 보편적으로 많이 사용한다.
- 맡은 일에만 집중할 수 있게 되기 때문에 효율성을 높이고 유지보수가 편리해지고,
- 애플리케이션의 확장성과 유연성이 늘어나고, 중복코딩의 문제점이 사라진다.
- 유저 인터페이스와 비지니스 로직을 분리시킨다.

###  

### **MVC패턴의 단점**

- View와 Model 사이의 의존성이 높다. 따라서 어플리케이션이 커질수록 복잡하고 유지보수가 어려워질 수 있다.

##  

 

## **MVP 패턴**

MVC패턴은 View와 Model 사이의 의존성이 높고, 이 의존성이 높기 때문에 어플리케이션이 커지면 커질 수록 더 복잡해지고 유지보수가 힘들어진다는 단점을 가지고 있다.

 

이런 MVC패턴의 한계점들을 극복하기 위해 MVP패턴이 등장했다,

 

MVP는 Model-View-Presenter의 약자로 Model과 View는 MVC와 동일하지만 Controller 대신에 Presenter가 존재한다.

 



![img](https://blog.kakaocdn.net/dn/bahr8O/btsl1IyyLXm/EwZjljKGR0SMIjkdq9Koxk/img.png)



 

위 사진처럼 MVC와 다르게 컨트롤러 대신에 Presenter가 View와 Model 사이를 중계해주고 있다.

따라서 Model과 View는 서로를 알 필요가 전혀 없이 Presenter만 가리키게 된다.

즉, View와 Model의 의존성은 사라지게 된다.

 

사용자들의 입력들은 View를 통해서 데이터를 Presenter에 요청하고 Presenter는 Model에게 데이터를 요청한다.

Model은 Presenter에게 응답해서 다시 View로 전송해서 화면에 나타내게 되는 동작 순서를 가지고 있다.

모델은 위 MVC패턴과 동일하며 뷰와 프리젠터에서 구성 요소의 변화가 있다.

- V(View) 기본적으로는 MVC와 같이 화면에 보여지는 요소를 맡는 것은 동일하나 Controller가 사라짐에 따라서 이제 사용자의 입력을 받는 역할을 겸하게 된다. MVC에서 Controller의 역할의 일부를 얻게 되었다고 이해하면 좋다.
- P(Presenter) View에서 요청한 정보로 Model을 가공하여 View에 전달해주는 부분이다. 본질적으로는 MVC의 컨트롤러와 같지만 뷰에 연결되는 것이 아니라 그냥 인터페이스라는 점이 다르다.

###  

### **MVP패턴의 구조**

#### **M (Model)**

> 어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분

####  

#### **V (View)**

> 사용자에게 보여지는 UI부분

####  

#### **P (Presenter)**

> View에서 요청한 정보를 Model을 가공하여 View에 전달해 준다. (View와 Model의 다리같은 존재)

 

### **MVP패턴의 동작 방법**



![img](https://blog.kakaocdn.net/dn/mvjul/btsl1IrK85L/foC3IfOmXvwNEdEVXoF04K/img.png)



1. 사용자의 Action들은 View를 통해 들어온다.
2. View는 데이터를 Presenter에 요청한다. 
3. Presenter는 Model에게 데이터를 요청한다. 
4. Model은 Presenter에서 요청받은 데이터를 응답한다. 
5. Presenter는 View에게 데이터를 응답한다. 
6. View는 Presenter가 응답한 데이터를 이용하여 화면을 나타낸다. 

 

### **MVP패턴의 특징**

- View를 통해 사용자 액션이 들어온다
- Presenter가 Model로부터 받은 데이터를 View로 넘겨준다.
- Presenter와 View가 1:1 관계에 있다

###  

### **MVP패턴의 장점**

- View와 Model의 의존성이 없다.
  - Model이 View에게 데이터를 직접 넘겨주는게 아니라 Presenter를 거쳐서 넘겨주기 때문
  - 즉, Presenter를 통해서만 데이터를 전달 받기 때문에
  - MVC와의 차이점

###  

### **MVP패턴의 단점**

- View와 Presenter 사이의 의존성이 높다.
  - View와 Model 사이의 의존성은 해결되었지만 대신에 View와 Presenter 사이에 높은 의존성을 가지게 되었다.
- Presenter와 View가 1:1 관계이기 때문에 중복코드가 많이 발생할 수 있다.
- 어플리케이션이 복잡해질수록 View와 Presenter 사이의 의존성이 더욱 강해지고 복잡해진다.
  - 이는 MVC와 마찬가지

##  

##  

## **MVVM 패턴**

View와 Model의 의존성이 없는 대신에 View와 Presenter가 의존성이 생겨버리고 그로인한 문제점을 극복하기 위해서 등장한 패턴이 바로 MVVM이다.

 

MVVM은 Model - View - ViewModel의 약자로 이번에는 MVP와 다르게 Presenter 대신 ViewModel이 존재한다.

 



![img](https://blog.kakaocdn.net/dn/cHFPN7/btsl6NyuE9B/uzEkYd61SggZjGg9yj2otk/img.png)



**VM(ViewModel)**

- 뷰에 필요한 데이터를 준비하고 모델에 필요한 이벤트를 전달한다.
- 그러면서도 뷰에 종속되지 않는 뷰만을 위한 모델이라고 할 수 있다.

 

여기서 궁금증이 들 수 있다. 어떻게 뷰와 뷰모델, 뷰모델과 모델간에 의존성이 사라지게 되느냐. 그것은 바로 Command패턴과 Data Binding 덕분인데, 이 패턴과 라이브러리로 인해서 의존성이 완전히 사라지게 된다.

 

Command패턴과 Data Binding은 각각 또 하나의 문서를 할애해서 설명이 필요할 만큼이나 긴 설명이 필요해서 해당 포스팅의 목적과 엇나갈 수 있으므로 간략하게만 짚고 넘어가자.

- Command패턴은 앞서 설명한 여러가지 디자인 패턴들 중에 하나이며 요청을 객체의 형태로 캡슐화하여 저장, 로깅, 취소를 할 수 있는 패턴이다.
- Data Binding은 XML에 만든 View들을 자동으로 알아서 만들어주는 안드로이드 라이브러리이다.

 

요약하자면 여전히 MVP패턴처럼 View를 통해 사용자의 입력이 들어오게 되면 Command패턴으로 ViewModel에 요청한다. ViewModel은 Model에게 필요한 데이터를 요청하고 Model은 응답한뒤 ViewModel에서 다시 가공해서 저장한다. 여기서 View로 다시 안돌려주냐고 할 수 있는데, View는 Data Binding을 통해 자동으로 갱신하게 된다.

 

안드로이드에서 가장 많이 사용되는 설계 패턴이다. 

###  

### **MVVM 패턴의** **구조**

#### **M (Model)**

> 어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분

####  

#### **V (View)**

> 사용자에서 보여지는 UI 부분

####  

#### **VM (View Model)**

View를 표현하기 위해 만든 View를 위한 Model이다.

> View를 나타내 주기 위한 Model이자 View를 나타내기 위한 데이터 처리를 하는 부분

###  

### **MVVM 패턴의 동작 방법**



![img](https://blog.kakaocdn.net/dn/lBQhU/btsl6NZwVV2/KJkFiLNjzVy0i0rYJ9kKa0/img.png)



 

1. 사용자의 Action들은 View를 통해 들어온다.
2. View에 Action이 들어오면, Command 패턴으로 View Model에 Action을 전달
3. View Model은 Model에게 데이터를 요청한다. 
4. Model은 View Model에게 요청받는 데이터를 응답한다. 
5. View Model은 응답 받은 데이터를 가공하여 저장한다. 
6. View는 View Model과 Data Binding하여 화면을 나타낸다.

 

### **MVVM 패턴의 특징** 

- Command 패턴과 Data Binding 두 가지 패턴을 사용하여 구현된다.
- Command 패턴과 Data Binding을 이용하여 View와 View Model 사이의 의존성을 없앴다.
  - View Mode과 View는 1:n 관계

###  

### **MVVM 패턴의 장점**

- View와 Model 사이의 의존성이 없다.
-  Command 패턴과 Data Binding을 사용하여 View와 View Model 사이의 의존성 또한 없앴다.
- 각각의 부분은 독립적이기 때문에 테스트와 모듈화가 쉽다.
- View와 Model을 연결하기 위해 사용해야 하는 연결 코드를 줄일 수 있다.

###  

### **MVVM 패턴의 단점**

- View Model의 설계가 어렵다.
- View가 변수와 표현식 모두에 바인딩될 수 있어서 시간이 지남에 따라 관계없는 프리젠테이션 로직이 늘어나 유지 관리하기 번거롭다.

------

참고 자료

https://velog.io/@ptm0304/MVC-vs-MVP-vs-MVVM

[https://shoney.tistory.com/entry/MVC-MVP-MVVM-%ED%8C%A8%ED%84%B4](https://shoney.tistory.com/entry/MVC-MVP-MVVM-패턴)

https://metafor.notion.site/54d624628a634c879cc93d94f54cd2d1#0c4b1ec1ee49475ebebbf3897e5d7818