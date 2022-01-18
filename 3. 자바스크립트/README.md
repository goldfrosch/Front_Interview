# Front_Interview 자바스크립트 관련

## 1. ES5 & ES6의 차이점

es5와 es6의 차이는 대표적으로 6가지가 존재한다.

- 템플릿 리터럴
- 화살표(arrow) 함수
- this
- 변수 선언
- 모듈
- 클래스

1.  템플릿 리터럴

    ES6부터 새로 추가된 기능으로 기존에는 하나의 String에 변수 값을 추가해줌으로써 해당 값들을 출력해주는데 사용해줬다면 현재는 `${variable}` 방식의 placeholder를 사용함으로써 문자열과 함께 표현식을 바로 넣어주는 것이 가능해졌다.

2.  화살표 함수

    이 역시 ES6부터 새로 추가된 방식으로 기존의 함수 선언식은 function() {} 방식이였다면 새롭게 만들어진 arrow함수는 이것을 조금 더 단순화 시켜서 var test = () => {} 방식으로 변경해 사용하기 쉽게 만들어줬다.

3.  this

    ES5의 경우에는 객체 내의 메소드를 실행 시 this는 메소드가 선언된 해당 객체를 가리키는 방식이였다. 하지만 객체 안에서 선언된 함수의 this는 해당 객체가 아닌 window를 바라보는 문제가 있어 함수안에서 this.var로 값을 불러오려고 해도 window.var이 되어버려 undefined가 나오는 문제가 되어버렸다.

    그 문제를 해결하기 위해 ES5에서는 innerInfo.call(this)라는 것을 통해 this를 바인드 해 출력해주는 방식을 이용했다.

    하지만 ES6에서의 this는 자신을 둘러싸고 있는 this를 바라보는 방식으로 변경이 되어 이전처럼 굳이 바인드하거나 변수에 담을 필요가 사라지게 되었다.

    생성자 함수의 인스턴스 같은 경우에 this는 인스턴스를 가르키고 화살표 함수를 사용할 경우 함수가 선언된 스코프에 자동으로 바인딩이 되는 장점이 있다.

4.  변수 선언

    ES5에서는 var라는 것밖에 존재하지 않았다. 재할당, 재선언에 굉장히 자유로웠지만 호이스팅이 발생하는 문제 또한 존재했다.

    ES6에서는 let, const라는 것이 추가가 되었다. let의 경우에 한번 선언된 변수에 동일한 이름으로 재선언이 불가능하게 되었다.

    ```
    let x = 0;

    let x = 12;

    //이게안되는 거임
    //var은 되는데
    //근데 이게 더 좋은듯?
    ```

    let과 const는 원래 사용하는 변수처럼 함수에 선언된 변수값은 외부에서 호출이 불가능하다.

    const의 경우는 한번 선언하면 끝 즉 자바에서 final과 비슷한 기능을 하는 것 같다. 한번 선언 후 값 변경이 불가능하다. 하지만 리액트에서는 useState를 이용해서 변경이 가능하게 해준다.

    let 하고 const의 경우에의 차이는 react에서 컴포넌트 내부에서 표시하는 값으로 사용할 때 let으로 사용해서 출력하려고하면 컴포넌트가 업데이트가 되지 않아 useState를 이용해 const의 값을 변경해줌으로써 컴포넌트를 업데이트 하는 방식의 hooks다

5.  모듈

    ES5의 경우에는 require를 통해서 모듈화가 가능했다. require의 경우에는 파일 자체를 import해서 사용하는 특징이 있었지만 ES6에서는 import export라는 것이 추가가 되어 특정 모듈을 import, export하는 특징이 존재한다.

6.  클래스

    ES5의 경우에는 함수 prototype을 이용해 비슷한 방식으로 실현이 가능했으나 ES6에서 추가가 되면서 super를 이용해 상속이 가능하다.

## 2. 디바운싱(Debouncing)과 쓰로틀링(Throttling)

디바운싱과 쓰로틀링은 프로그래밍 기법 중 하나

- 디바운싱

  연이어 호출되는 함수들 중의 가장 마지막 함수만 호출되도록 하는 것을 의미

- 쓰로틀링

  마지막 함수가 호출된 후 일정 시간 동안 호출되지 않도록 막는 것

주로 스크롤 이벤트에서 많이 사용이 되는 기법으로 자바스크립트에서는 setTimeout을 이용해서 해당 이벤트들을 처리한다

디바운싱 예제

```
  let timer;
  document.querySelector('#input').addEventListener('input', function(e) {
      if (timer) {
          clearTimeout(timer);
      }
      timer = setTimeout(function() {
          console.log('시간은 움직였다');
      }, 200);
  })
```

특정 이벤트가 발생할 때 마다 이렇게 timeout을 한 변수에 계속 선언해줌으로써 timeout을 초기화 시키고 동시에 마지막을 기점으로 선언된 timeout 이벤트 하나만을 선언시켜주는 기법

쓰로틀링 예제

```
  let timer;
  document.querySelector('#input').addEventListener('input', function(e) {
      if(!timer) {
          timer = setTimeout(function() {
              timer = null;
              console.log("쿨타임 다 됨?");
          },200);
      }
  })
```

이런식으로 timer라는 변수가 null일 경우에 0.2초 후에 timer가 null이 되게하는 함수를 만들어줘 이벤트를 선언할 때마다 null인지 아닌지를 검증해주고 null일 경우에만 이벤트를 진행시키는 기법이다.

스크롤 이벤트에서 많이 쓰이기 좋은 기법 같다.
