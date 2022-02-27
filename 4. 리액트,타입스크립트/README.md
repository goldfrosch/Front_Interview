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
    skills: string[];
  }

  type GoldFrosch = Person & Developer;

  //결과값
  {
    name: never;
    age: number;
    skills: string[];
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

## 5. Life Cycle

- componentDidMount

  컴포넌트가 첫 렌더링을 마치고 나면 호출되는 메소드

  이 메서드가 호출되는 시점은 우리가 만든 컴포넌트가 화면에 나타날 경우다.

- shouldComponentUpdate

  컴포넌트가 리렌더링 할지 말지를 결정하는 메소드, 보통 최적화할 때 많이 사용하며 useMemo랑 비슷한 역할을 수행 함

- componentDidUpdate

  리렌더링을 마치고 화면에 우리가 원하는 변화가 모두 반영되고 난 뒤 호출되는 메서드

  파라미터는 prevProps, prevState, snapshot으로 3번째 파라미터에서는 반환한 값을 조회 할 수 있다.

- componentWillUnmount

  컴포넌트가 화면에서 사라지기 직전에 호출되는 메소드
  일반적으로는 setTimeout나 DOM에 직접적으로 등록한 메소드를 지우는 역할을 함

- useEffect

  클래스형 컴포넌트가 아닌 함수형 컴포넌트에서 상태관리를 위해 항상 사용하는 hooks이며 각각 마운트, 업데이트, 언마운트를 하나의 hooks로 처리하는 간편함이 있다.

  마운트, 언마운트 시

  마운트, 언마운트 시에 보통 넣는 함수들은 정해져있다.

  - 마운트 시

    - props로 받은 컴포넌트 로컬 상태 설정
    - 외부 API 호출
    - 라이브러리 사용 호출
    - setInterval, setTimeout같은 작업 예약 호출

  - 언마운트 시
    - setInterval, setTimeout같은 작업 clear
    - 라이브러리 인스턴스 제거

  ```
  useEffect(() => {
    console.log("마운트 됨");
    return () => {
      console.log("언마운트 됨");
    }
  },[]);
  ```

  기본적으로 useEffect의 배열(deps 라고 부르는 듯 하다) 안에 값이 없으면 일반적인 마운트 언마운트 형식으로 작동하며 처음에 작성하는 함수가 마운트 시 return안에 넣는 함수들이 언마운트 되는 시점에서 동작하는 것들이다.

  업데이트 시

  ```
  useEffect(() => {
    console.log('user 값이 설정됨');
    console.log(user);
    return () => {
      console.log('user 가 바뀌기 전..');
      console.log(user);
    };
  }, [user]);
  ```

  배열(deps)값에 집어넣음으로써 배열안의 값이 업데이트 될 때마다 그리고 return으로 언마운트 될 때도 동작하게 된다.

  마지막으로 deps를 아에 생략하게 될 경우는

  ```
  useEffect(() => {
    console.log("HI BRO");
  })
  ```

  컴포넌트가 리렌더링 될 때 마다 호출하게 된다.
  
  그래서 위의 경우에 setState같은 리렌더링하는 함수를 넣어버리면 무한으로 즐기는 맛집이 되는 것 이다.
