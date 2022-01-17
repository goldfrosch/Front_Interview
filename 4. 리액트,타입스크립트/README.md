# Front_Interview React, TypeScript

## 1. Typescript 색인 타입

코드의 실행 시점에서만 알 수 있는 동적 타입으로 전 면접에서 API에서 호출할 때 API형식이 다를 때 어떻게 하냐에 대한 대답을 이것을 원했나 싶은 것

```
interface NameHeightMap {
  [userName: string]: number | undefined;
}
```

이런식으로 key값에 타입을 선언한 변수로 지정하고 해당 key값이 존재하냐 안하냐에 따라 number값의 타입인지 아니면 undefined의 타입인지로 결정하는 방식이다.
API의 타입이 다를 때 하는 방식에 대해 물어볼 때는 색인 타입도 같이 생각하면 좋을 것 같다

## 2. Union, Intersection Type

any는 너무 광범위하고 특정 타입들을 지정해주기에 매우 애매하다.

그러므로 특정 타입들을 여러개 지정하고 각 타입들마다 처리하는 방법도 다르게 해줘야 할 필요가 있다.

그것을 위해서 있는 방법이 유니온, 인터섹션 타입이다.

- 유니온 타입

  유니온 타입은 특정 타입 or 특정 타입 이라고 선언해 주는 방식이다.

  ```
  const testBro = (test: number | string) => {
    if(typeof test === 'number') {
      console.log("hi 숫자맨");
    }
    if (typeof test === 'string') {
      console.log("hi 문자맨");
    }
    return new TypeError('test는 숫자 아님 문자외에는 못씀');
  }
  ```

  위의 예제처럼 여러 타입에 대한 대처가 유연하게 가능하게 해주는 대표적인 방법이다.

- 인터섹션 타입

  인터섹션 타입의 경우에는 여러개의 타입을 합집합처럼 겹치게 해준다라는 표현이 가장 맞는 것 같다.

  ```
    interface Person {
      name: string;
      age: number;
    }

    interface Developer {
      name: string;
      skill: string[];
    }

    type GoldFrosch = Person & Developer;
  ```

  해당 코드에 따르게 될 시 GoldFrosch라는 타입은

  ```
  {
    name: string;
    age: number;
    skill: string[];
  }
  ```

  라는 속성값으로 지정이 되는 것이다.

  하지만 동일 키값을 가졌지만 다른 타입 속성을 가진 경우에는 never 속성으로 변경이 된다.

  ```
  interface Person {
    name: string;
    age: number;
  }

  interface Developer {
    name: number;
    skill: string[];
  }

  type GoldFrosch = Person & Developer;

  //결과값
  {
    name: never;
    age: number;
    skill: string[];
  }
  ```

  이 점을 주의하며 사용하면 좋은 방법이 될 것 같다.

## 3. 제네릭

제네릭의 경우 C#, Java등에서도 자주 이용해먹는 특징으로 재사용성을 고려해 다양한 object가 들어가도 사용이 되게끔 설정해두는 것을 의미한다.

일반적으로 any를 이용해서 하는 방법도 있지만 타입스크립트는 any스크립트가 아니다. any사용은 거의 없도록 하고 재사용성을 고려한 것들은 제네릭을 쓰는 것이 맞다.

any를 사용하면 안되는 대표적인 이유는 타입 검증이다. any를 사용하게 되면 모든 타입을 다 허용해주는 것이기에 일반적인 타입에러도 관대하게 넘어가줄 수 있는 문제가 되기 때문이다.

하지만 제네릭을 사용하면 그 부분이 최소화될 수 있다.

예시

```
  function test(text: any){
    return text;
  }

  function test<T>(text: T): T{
    return text;
  }
```

위의 함수와 밑의 함수의 결정적인 차이는 return의 타입 종류다. 현 예시는 기본적인 return인지라 크게 문제가 되지는 않을 수 있다.

하지만 함수가 복잡해지고 받아와야할 데이터가 T타입과 동일해야할 때 첫번째 함수를 쓰게될 시 문제가 발생하게 된다.

그런 문제를 해결하기 위해 제네릭을 쓰는 것이 옳다고 볼 수 있다.

## 4. Redux

한 곳에 데이터를 저장하고 그 데이터를 편하게 갖다쓰기 위한 방법 중 대표적은 것으로, store라는 하나의 데이터 공간을 보유하고있으며, 액션이라는 객체를 통해서만 데이터가 변경이 가능하며, 변경은 오직 순수한 함수로만 가능한 것이 리덕스라는 것이다.

- store

  Store는 상태가 관리되는 오직 하나의 공간을 의미한다.
  컴포넌트와는 별개로 스토어라는 공간이 있어 그 안에서 필요한 데이터를 가져올 수 있는 역할을 해준다.

- action

  Action은 앱에서 스토어에 운반할 데이터를 말하며 자바스크립트 객체 형식으로 이루어져있는게 주요 특징이다.

- Reducer

  Action을 받아 Store의 상태값을 변경해주는 중간 처리 장치를 의미하며 dispatch() 메소드를 사용해야한다.

  Redux는 스토어라는 공간 안에서 디스패치를 통해 액션을 선언 그리고 액션을 통해 reducer가 스토어를 변경 후 업데이트 하는 것이 기본 원리다.
