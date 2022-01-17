# Front_Interview React, TypeScript

## 1. 색인 타입
	코드의 실행 시점에서만 알 수 있는 동적 타입으로 전 면접에서 API에서 호출할 때 API형식이 다를 때 어떻게 하냐에 대한 대답을 이것을 원했나 싶은 것
	```
	interface NameHeightMap {
	  [userName: string]: number | undefined;
	}
	```
	
	이런식으로 key값에 타입을 선언한 변수로 지정하고 해당 key값이 존재하냐 안하냐에 따라 number값의 타입인지 아니면 undefined의 타입인지로 결정하는 방식이다.
	API의 타입이 다를 때 하는 방식에 대해 물어볼 때는 색인 타입도 같이 생각하면 좋을 것 같다