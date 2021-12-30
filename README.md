# Front_Interview 필수 요소

## 1. 브라우저 저장소

 - 웹 스토리지(세션, 로컬 스토리지)
  HTML5부터 추가 된 저장소로 key, value인 해시맵 형태로 구성되어 있다.
  
  세션과 로컬 스토리지의 차이는 영구성이다.
  
  세션은 브라우저 종료 시 사라지지만
  로컬은 브라우저가 종료되도 저장되어있다.
  
  String 형태로 저장을 해야하기 때문에 객체는 기본적으로 JSON.stringify를 이용해 string화 시켜 저장하고
  JSON.parse를 이용해서 객체화 시켜서 사용한다.
 
 
 - 쿠키
  대부분의 브라우저가 지원해주는 저장소
  
  매번 HTTP요청마다 Request로 보내야 하기에 서버에 부담이 늘어난다
  용량이 매우작다 (약 4kb)
  만료 기간이 존재해 특정 시간이 지나면 만료가 가능하게 할 수 있다


## 2. 자바스크립트에서의 this
  
  this는 매우 유동적으로 사용할 수 있다.
  기본적으로 전역 함수에서 선언하는 this는 window를 가르킨다
  ex)
  let a = 100;

  console.log(window.a) // 100
  console.log(this.a) // 100

  엄격 모드라는 것이 존재한다. 엄격 모드는 말그대로 엄격하게 관리 한다 라는 의미이며
  문법을 올바르게 지키지 않는 이상 undefined가 됩니다.
  
  ex)
  function exam1() {
   return this;
  }
  
  console.log(exam1() === window) // true
  console.log(exam1() === global) // true
  
  만약 여기에 엄격모드가 들어갈 시
  function exam1() {
    "use strict";
    return this;
  }
  
  console.log(exam1() === window) // false
  console.log(window.exam1() === window) // true
  
  this는 위치에 따라서 인식되는 범위가 다르다
  1. 함수에서의 this -> 기본적으로 window임
  2. 메소드에서의 this -> 메소드를 실행하고 있는 객체를 기준으로 함
  3. 생성자에서의 this -> 생성자는 자바처럼 반드시 new 객체() 로 선언을 해줘야 하며 생성자에서의 this는 만들어 질 새 객체가 중심이 된다.
  4. 객체에서의 this -> 객체를 가르킨다
  5. 간접 실행에서의 this -> call(), apply()의 메소드를 호출하는 것을 의미하며 call()은 주어진 this값 및 각각 전달된 인수와 함께 함수를 호출해준다.
     / apply()는 주어진 this값과 배열로 제공되는 arguments로 함수를 호출한다.
    ex)
    function add(c, d) {
      return this.a + this.b + c + d;
    };
    
    let variable = {
      a: 1,
      b: 3,
    };
    
    add.call(variable, 5, 7); // this로 사용할 객체를 variable로 지정했기에 this.a = 1, this.b = 3으로 총 16이라는 결과물이 나온다.
    add.apply(variable, [10, 20]); // call과 마찬가지로 처음에 variable은 this로 사용할 객체, 두번째 인자인 배열은 함수에 들어갈 인자들로
    //this.a = 1, this.b = 3이라는 결과가 도출된다. 1 + 3 + 10 + 20 총 34라는 결과
    
  6. 바인딩 함수에서의 this -> bind()메소드를 호출해서 사용하는 경우로 bind()는 새로운 함수를 생성하는 방식으로 "strict mode"일때와 아닐 때가 또 다르다
    ex)
    const module = {
      x: 42,
      getX: function() {
        return this.x;
      }
    };
    
    const unboundGetX = module.getX;
    console.log(unboundGetX()); // this.x를 가르키는 것은 그냥 함수로 설정이 되 전역 변수인 x는 존재하지 않아 undefined로 출력된다.
    
    const boundGetX = unboundGetX.bind(module);
    console.log(boundGetX()); // 전역으로 선언된 unboundGetX를 boundGetX에서 module의 getX를 호출했기에 return이 올바르게 42로 출력이 된다.
    
  7. 화살표 함수에서의 this -> 화살표 함수는 간단한 형태로 정의하거나 혹은 문맥을 바인드 하기 위해 주로 사용되는 함수
  
    ex)
    let person = {
      name: "youngjin",
      getName: function (){
        console.log(this); // 객체 변수인 person을 가르친다;
        setTimeout(() => {
          console.log(this); // 객체 변수인 person을 가르친다
          console.log(this.name) //person.name => youngjin를 출력한다.
        }, 1000);
      }
    }
    
    person.getName();
 
   일반 함수의 this와 화살표 함수의 this의 차이
   
   자바스크립트에서의 함수에서는 어디서 선언되든 this는 전역 객체(window)를 가르킨다.
   화살표 함수의 this는 언제나 상위 스코프의 this를 가르킨다
 
