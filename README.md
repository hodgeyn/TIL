# TIL
Today I Learned


2019년 10월 5일 
-------------
ㅇ 빈 객체 여부를 확인하는 방법  

1. Object.keys(obj).length === 0
2. 빈 객체 체크 해서 확인하는 함수 작성
for (let prop in obj) {
  if (obj.hasOwnProperty(prop)) {
    return false  // 아닌 경우 true
  }
}

ㅇ 해당 프로퍼티가 있는 지 확인하려면
Object.hasOwnProperty('prop') // return Boolean



2019년 10월 6일
-------------

ㅇ setState 작동방식
- setState() / 상태변화에 대한 정의 -> render() / 변화 적용
  * 변화 적용을 위해서 jsx 문법을 사용하며, 이 문법을 통해 virtual dom 에 적용됨.
  -> virtual dom -> real dom 실제 dom 과 비교해서 다른 점만 비교하고 -> 진짜 그린다.
  
ㅇ 라이프 사이클
- 처음에 constructor 로 state 가 초기화 되며 render 가 실행, 실행된 내용이 화면에 표시가 된
이후 componentDidMount() 메소드가 실행
- 변화가 발생하면, setState -> render() -> componentDidUpdate()

2019년 10월 7일
---------

ㅇ 모든 이벤트 핸들러는 모든 브라우저에서 동일하게 처리하기 위하여 합성 이벤트 객체를 전달받게 되고, 풀링(기능을 사용하기 위한 준비 / 리소스 많이 차지함)
상태이고, 성능 상의 이유로 호출되고 나면 초기화되며, 동기 처리되는 특징을 가지고 있다.
ㅇ 이를 컨트롤 하고 비동기 처리해주기 위한 기능이 Throttle, debounce 등이다.

ㅇ 프레임워크와 라이브러리 차이
- 프레임워크 : 특정 디자인 패턴이나 전처리 후처리에 필요한 동작과 기능을 수행하기 위해서 프레임워크가
중간 중간에 특정 비즈니스나 특정 구현 단에서만 사용자의 코드를 검색하여 사용하는 형태(제어의 역전 발생)
- 라이브러리 : 함수, 기능 모음을 단순히 가져다쓰는 

2019년 10월 8일
----------

ㅇ node core modules 
- node 와 함께 번들링되어 있는 모듈, require 방식으로 사용이 가능하다. (fs, http, url, path)
ㅇ 이벤트와 콜백 구분(비슷)
- 콜백함수는 비동기식 함수에서 결과를 반환할 때 호출
- 이벤트 핸들링은 옵저버 패턴에 의해 작동. / Eventemitter (node 에 내장된 일종의 옵저버 패턴)
* 이벤트를 내보내는 모든 객체는 Eventemitter 클래스의 인스턴스, On 메소드 사용 가능
- Http 모듈에서 서버 생성, 응답 시 response 는 EventEmitter 클래스를 상속한 객체로
on 메소드 사용 가능


2019년 10월 9일
----------

ㅇ 여러 개의 마이크로 서비스로 구성된 서버사이드, React 이용한 Single Page App 으로
서비스 구성 시 CORS 이슈에 직면하게됨

ㅇ CORS : Cross Origin Resource Sharing / 해당 페이지를 제공한 서버가 아닌
다른 서버의 자원을 호출하는 것을 의미

ㅇ client 의 일반적인 요청이 아닌 경우, 리소스 보관 서버에 preflighted 요청을 보냄
preflighted 요청은 특별한 요청으로 method = options 로 전송

ㅇ response 의 writeHead 메소드 : 상태코드 와 헤더를 모두 작성한다. 

ㅇ CORS 이슈에 대해 각 브라우저는 정의가 되어 있고, 대응이 가능함.

2019년 10월 10일
----------

ㅇ 서버 post, get 요청에 대해 바디 데이터에 접근할 때
Request 를 사용한다. ReadableStream 인터페이스 구현하기 때문에,
이 스트림에 이벤트 리스너를 연결할 수 있다.
'data', 'end'

ㅇ 이벤트 리스너란 이벤트가 발생했을 때, 그 처리를 담당하는 함수를 말하며,
이벤트 핸들러라고도 한다.

ㅇ 리액트에서 data 를 상위 컴포넌트, 하위 컴포넌트 간
전달 이동하기 위해서(데이터의 변화를 반영하는 것 포함)
데이터 변화를 위해서 렌더링이 이루어져야 하는데,
기존 데이터에 push 를 하는 경우, 주소 값이 변경되지 않아서 렌더링이 이루어지지
않고, concat 메소드를 통해 주소값이 변경된 새로운 배열이 만들어져야만
렌더링이 발생함을 꼭 기억!


2019년 10월 11일
-----------------
ㅇ Node.js 에서 스트림은 한 지점에서 다른 지점으로 이동하는 일련의 데이터를 의미
* 중요한 핵심은 모든 데이터가 전부 다 사용가능 할 때
ㅇ 데이터가 이동할 때 버퍼(청크) 단위로 이동, 파일 시스템에서 바이너리 데이터가 이동하는 것을 의미
ㅇ Buffer 로 들어온 데이터에 대해서 디코딩을 위해서
- JSON.parse(buffer) 도 가능하고, JSON.parse(buffer.toString()) 도 가능
ㅇ 데이터의 스코프에 대해서 항상 유의하기를 바란다.


2019년 10월 12일
------------

ㅇ 파일 시스템에서 파일을 읽어올 때 데이터는 RAW DATA(BUFFER) 형식으로 불러옴.

ㅇ JSON.parse 를 통해 JSON 포맷으로 불러올 수 있다.

ㅇ 파일 시스템의 경우, 사용하지 않는 것과 비교해 response 규칙을 어느 정도 유연하게 가져갈 수 있음.

ㅇ 콘솔 많이 찍어보는 것의 중요성을 다시 한번 더 확인함.

ㅇ 서버 쪽과 연계하여 혹은 독립적으로도 클라이언트 함수의 관계를 명료하게 효과적으로 가져갈 수 있도록 
무수한 설계를 해봐야 한다는 것을 다시 느낌.

2019년 10월 14일
----------
ㅇ 코드 패턴 익히기
```js
var depthFilter = function (filterDepth) {
  return function(node, nodeDepth) {
    return filterDepth === nodeDepth;  
  };
};
```
이런 것을 통해 두 함수 내에 인자의 값이 같은 지 확인할 수 있음.


ㅇ 프로미스 내 resolve (value) 를 통해 다음 .then 의 인자로 value 를 전달할 수 있다.
