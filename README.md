공부공부공부공부

복습 필요한거

### 클로저, 스코프

- 스코프: 영어 자체의 뜻이나 자바스크립트나 동일하게 범위라는 의미를 가지고 있다. 자바스크립트에서의 정의는 식별자 접근 규칙에 따른 유효 범위로 변수, 함수, 클래스에 접근할 수 있는 범위가 존재하며 중괄호(블록)이나 함수에 의해 나뉘어지게 되는 그 범위를 스코프라고 정의한다.

- 스코프의 규칙

  - 안쪽 스코프에서 바깥쪽 스코프는 접근이 가능하나 바깥쪽의 스코프에서 안쪽의 스코프는 접근이 불가능하다.
  - 스코프는 중첩이 가능하다.
  - 가장 바깥의 스코프는 전역 스코프, 나머지는 전부 지역 스코프라고 정의한다.
  - 지역 변수는 전역 변수보다 우선순위가 더 높다.

  전역 변수는 무조건 최소화 하는 것이 좋다. 가장 바깥쪽의 스코프인지라 어디서든 접근이 되기 때문에 의도하지 않은 로직에 의해 문제가 발생하는 이슈가 생길 수 있어 최대한 사용하지 않는 것이 중요하다.

- 클로저: 함수를 지칭하고 그 함수가 선언된 환경과의 관계라는 개념이 합쳐진 의미, 클로저의 핵심은 클로저는 내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것을 가리킨다 스코프는 내부에서 외부는 접속이 가능하지만 외부는 내부를 접속하지 못하는 것을 이용하는 것이 핵심. 클로저는 자바스크립트에서만 통용되는 것이 아닌 함수형 프로그래밍 언어에서 공통적으로 발견되는 특성이다.

### stateless

- 클라이언트와 서버 관계에서 서버가 클라이언트의 상태를 보존하지 않음을 의미
- 장점: 서버의 확장성이 높아 대량의 트래픽 발생 시에도 대처를 수월하게 가능함
- 단점: 클라이언트의 요청에 상대적으로 stateful보다 더 많은 데이터가 소모된다.

### 불변성

- 사전적인 정의는 말 그대로 한번 생성되고 나면 그 뒤에는 변할 수 없는 것
- 원시 타입(boolean, string, number... etc)는 불변한다. 즉 메모리 영역 안에서 변경이 불가능하고 변수에 할당할 때 완전히 새로운 값이 만들어져서 재 할당하게 된다.
- 즉 원시 타입 형태는 불변성 때문에 변환 시 새롭게 재 할당이 되지만 그 외의 객체들은 변할 수 있는 값이 되기 때문에 새로운 값이 만들어져 재할당 되지 않고 직접 변경이 자유롭게 가능하다.

### OSI 7계층 (설명 추가 필요)

- 1계층: 물리 계층
- 2계층: 데이터 링크 계층
- 3계층: 네트워크 계층
- 4계층: 전송 계층
- 5계층: 세션 계층
- 6계층: 표현 계층
- 7계층: 응용 계층

### jwt

jwt는 세파트로 나누어져있어 header(헤더), payload(페이로드), signature(서명) 총 3가지로 나뉘어져 있으며 base64형태로 인코딩 되어 나오게 된다.

jwt의 장점은 사용자 인증에 필요한 모든 정보가 토큰 자체에 포함되어 있어 별도의 인증 저장소가 필요하지 않다라는 것.
하지만 클라이언트에 저장되어 데이터베이스에서 사용자 정보를 조작해도 토큰에 직접 적용을 할 수 없다는 것이 문제며 필드값이 커지면 토큰이 커질 수 있다.

### 전역 변수의 문제점

- 암묵적 결합: 전역 변수는 모든 코드가 전역 변수를 참조하고 변경할 수 있는 암묵적 결합을 허용한다. 즉 유효범위가 크면 코드의 가독성이 나빠지고 의도치 않게 상태가 변경되어 위험성이 높아진다.

- 긴 생명 주기: 긴 생명 주기로 인해 메모리 리소스도 오랜 기간 소비하고, 상태 변경에 의한 오류가 발생할 확률이 높다.

- 스코프 체인 상에서 종점이 존재: 스코프 체인 상에서 종점이 존재하기 때문에 가장 마지막에 검색이 된다. 즉 검색 속도가 가장 느리다.

- 네임스페이스 오염: 자바스크립트의 문제 중 하나로 파일이 분리되어 있다고 해도 전역 스코프를 공유한다. 따라서 다른 파일 내에서 동일한 이름으로 전역 변수나 전역 함수를 재할당 할 경우 예상치 못한 결과를 가져올 수 있다.

### 제너레이터 함수

- Generator Function는 사용자의 요구에 따라 다른 시간 간격으로 여러 값을 반환할 수 있으며, 내부 상태를 관리할 수 있는 함수다. 그래서 사용자의 요구에 따라 일시적으로 정지될 수도, 다시 시작될 수도 있다. 핵심 기능은 함수를 작성 할 떄 함수를 특정 구간에 멈춰놓을 수도 있고, 원할 때 다시 돌아가게 할 수도 있습니다. 그리고 결과값을 여러번 반환 할 수도 있습니다
