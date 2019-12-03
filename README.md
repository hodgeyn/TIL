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


2019년 10월 15일
---------

ㅇ EXPRESS 는 자체적인 최소한의 기능을 갖춘(가벼운) 라우팅 및 미들웨어 웹 프레임워크이다.
Express 애플리케이션은 일련의 미들웨어 함수 호출이다.

ㅇ 미들웨어 함수는 요청 오브젝트(req), 응답 오브젝트(res), 요청-응답 주기 중
그 다음 미들웨어 함수에 대한 엑세스 권한을 갖는 함수

ㅇ app.use() 또는 app.method() 함수를 이용해 미들웨어를 바인딩 시킨다. 

2019년 10월 16일
-------
ㅇ server 에서 controllers, db, models 로 구분되는 것

ㅇ db 에서 connection 을 만들어주었다면, 이를 module.exports 를 통해 외부로 보냄

ㅇ 이것을 require 로 받아올 수 있음.

ㅇ Express 는 비동기 기능을 제공하고 있어, Promise 를 통해 통신의 요청과 응답을
통해 대응할 수 있다. 


2019년 10월 17일
--------

ㅇ 브라우저에서 유저의 액션이 일어나면, 설정된 엔드포인트로 이동할 때, 라우터를 통해 분기가 가능함과 동시에,
라우터는 엔드포인트에 맞는 컨트롤러 함수들을 부른다.

ㅇ 뷰는 컨트롤러를 통해 얻은 데이터 리소스를 가지고 다이나믹 하게 변경해서 보여줄 수 있다. 


2019년 10월 18일
-----------

ㅇ 세션과 쿠키의 요약

- 사용자가 로그인을 한다 (로그인 정보를 서버로 request)

- 서버가 request 가 들어오면 DB 쿼리를 통해 사용자를 검증하고 유효할 경우
고유한 ID 값을 부여하여, 세션 저장소에 저장한 후 이와 연결되는 세션 ID 를 생성하여
response header 에 포함시켜 반환한다.

- 사용자는 서버에서 해당 세션ID를 받아 쿠키에 저장을 한 후, 제한된 end point(인증이 필요한 요청)에 접근할 때 마다
쿠키를 request header에 포함시켜 보낸다.

- 서버에서는 쿠키를 받아 세션 저장소에서 검증한 후 요청에 해당하는 데이터를 반환한다.


2019년 10월 19일
----------------

ㅇ git repository 올리는 이슈와 관련 환경변수를 사용할 수 있다. (.env)

ㅇ npm install --save dotenv

ㅇ 프로젝트 루트경로에 .env 파일 생성하고 다음과 같이 작성 (변수명 = 값)
- SERVER_PORT = 3000
- DB_HOST = localhost
- DB_USER = root
- DB_PASSWORD = password

ㅇ 프로젝트 상단에 환경 변수 불러옴
- require('dotenv').config()

ㅇ 아래와 같이 사용
- db.connect ({
  host : process.env.DB_HOST,
  username : process.env.DB_USER,
  password : process.env.DB_PASSWORD
}); //DB 연결 예제


2019년 10월 20일
-----------

ㅇ setTimeout 함수 
- 첫번 째 인자 : 함수(promise 의 resolve, reject 포함) 또는 문자열이 들어갈 수 있다.
- 두번 째 인자 : 기다려야 할 ms 단위의 시간, 생략하면 0으로 인식
- 세번 째 인자 : 타이머가 만료되고 func 에 전달되는 추가적인 매개변수

ㅇ Promise.all 기능
- Array 와 같이 순회 가능한 객체를 입력받을 수 있음.
1. 프로미스 객체의 resolve 인자로 들어간 그 값을 불러올 수 있다.

2. 숫자 및 문자열도 요소로 쓰일 수 있다.

3. 생성된 프로미스 인스턴스를 통해 resolve 함수의 인자값을 리턴해줄 수 있다.

- 순회 가능한 객체가 비어있는 경우에만 동기적으로 이행 / 나머지는 비동기적으로 실행

- then 을 통해 Pending 상태의 promise 가 실행된다.


2019년 10월 21일
-------

ㅇ 자바스크립트는 프로토타입 기반 언어. 객체지향언어임.
Java, Python, Ruby 등 객체지향언어에서 Class 개념이 들어있지만, 자바스크립트는 아님

ㅇ 자바스크립트는 프로토타입을 통해서 상속을 흉내내고, ES6 에서 Class 문법이 추가되었지만,
클래스 기반인 것은 아님.

ㅇ 함수와 new 키워드를 통해 클래스를 흉내낼 수 있다.
공통적으로 가지고 있는 속성을 반복해서 사용하면, 메모리 낭비로 이어질 수 있으니,
이를 프로토타입으로 해결한다.

2019년 10월 22일
------

ㅇ 해시함수란 데이터의 효율적 관리를 목적으로 고정된 길이의 데이터로 매핑하는 함수

ㅇ 원래 데이터 값을 키, 매핑 후 데이터 값을 해시 값, 매핑하는 과정 자체를 해싱

ㅇ this 키워드
- 전역 또는 함수에서 this 가 호출되는 경우 window 를 가리킨다.
- call or apply 메소드 호출을 할 때 첫 번째 인자가 this.
- 구조체로 New 키워드를 사용하면, this 는 새로운 인스턴스를 가리킴.
- 메소드로 호출될 경우 this 는 호출한 부모 객체를 가리킨다.

2019년 10월 24일
------
ㅇ 리액트에서 map 함수를 쓸 때에는 내부에서 return 이 필수적이다. 다수의 props를 전달할 때는
key 설정이 필요한데, 해당 페이지에서 사용할 때는 key를 어떻게 전달해야 하는 지는  


2019년 10월 25일
---

ㅇ Jsx 문법에 && 조건문이 있다. 조건을 만족하면 뒤에 태그로 구성된 내용 실행할 수도 있다. 

2019년 10월 26일
-----

ㅇ onClick 자신을 콜백으로 부르는 경우 인자값에 이벤트 정보들이 들어가고, target 등 필요한 리소스를 연결해서 사용하면 됨. 


2019년 10월 27일
----

ㅇ 바닐라 js 는 순수한 자바스크립트로 프로그램 세계에서는 부가기능을 제외한 
기본적인 기능만 구현한 상태

ㅇ 리액트에서 애플리케이션을 만들 때, 하나의 루트 컴포넌트(App.js) 에서 상태를 관리한다.
대부분 작업을 할 때 부모 컴포넌트가 중간자 역할을 한다.

ㅇ 컴포넌트끼리 직접 소통하는 방법은 코드가 많이 꼬여서 절대 권장되지 않음.

ㅇ 그러나, 하나의 컴포넌트가 관리하는 것은 앱의 규모가 커졌을 때 유지보수가 쉽지 않음.
=> 리덕스 사용, 상태 관리를 외부에서 하는 방식

2019년 10월 28일
-------

ㅇ 협업에서 프리티어, 린트, 각 라이브러리 모듈의 버전 일치화 필요

ㅇ 미로라는 툴이 동시에 작업하기에 좋음.

2019년 10월 29일
--------

ㅇ 팀 프로젝트 중 Stack, Front-Back 의 스택 모듈 버전 맞추기

ㅇ 멤버 role 정하기

ㅇ 기간 및 구현할 수 있는 범위 정의

ㅇ Client 및 Server 구조 디자인

ㅇ API 명세서, Git rules, Task 


2019년 10월 30일
------

ㅇ 엔지니어는 커뮤니케이션을 잘하는 사람.

ㅇ 설치 모듈 다운그레이드 하는 방법
- npm install node@<version>
- 안 될 경우 글로벌로
  npm install -g npm@<version>
  npm install -g node@8.10.0
  
ㅇ 브랜치로 파일을 생성했을 경우에는
클론할 때도 브랜치 이름을 일치시켜야 한다.(중요)

- git clone -b <브랜치 명> 깃 주소

2019년 10월 31일
------

ㅇ .env 파일을 github 으로 푸시하는 것은 피해야 함. 

ㅇ Node.js 는 사용자가 사용할 수 있는 모든 환경변수를 포함하는 전역변수 process.env 


2019년 11월 1일
-------------

ㅇ db 한글(utf-8)로 설정 바꾸는 방법
show create table Concerts; // latin 으로 되어있지 않은 지 확인
alter table Concerts convert to character set utf8;

ㅇ 브랜치를 만들어서 관리하고 있다면, 
ec2 서버에서 git clone -b <브랜치 명> 깃 주소로 입력하면 된다.


2019년 11월 2일
----------

ㅇ Express 라우트 분기의 경우 동적인 값을 사용할 때는 '/:id(eg)' 으로 구분하고 req.params 로 
받아옵니다. 흔히 알고 있는 쿼리 스트링(?id = 12)은 일반 스트링 변수에서 사용할 수 있는 것으로 보입니다.

ㅇ 시퀄라이즈 조인을 위해서는 find 중첩은 Syntax 에러로 오류를 내고, association 을 사용해야 합니다.
N : N 의 경우 두 테이블에서 belongsTomany 사용하고 연결해주는 테이블에서는 belongsto 를 사용합니다.  

2019년 11월 3일
----------

ㅇ 시퀄라이즈에서 (뿐만 아니겠지만) 보통 id에서 auto_increment 를 사용하는 경우 
해당 id 값은 key 로 정의되어야 합니다.

ㅇ (시퀄라이즈) 외래키로 사용하고자 하는 것은 기본키로 정의되어야 한다. 

ㅇ 시퀄라이즈 문법에서 테이블에 insert 등 이루어질 때 칼럼명을 정확히 일치시켜야 합니다 꼭 명심.

2019년 11월 4일
---------

ㅇ 익스프레스 delete 요청 처리해줄 수 있는 부분이 있고, 시퀄라이즈로 해당 db 처리할 때에는 destroy를 
사용.

ㅇ destroy 메소드 다음에 then 콜백함수 사용 및 return 으로 delete 응답을 마무리하자.


2019년 11월 5일
---------
ㅇ 크롤링과 관련하여 cheerio 와 require 모듈을 사용하였음.

ㅇ 크롤링도 웹 페이지에서 요청을 받아오는 것이므로 비동기 처리가 필요한데 이를 위해서 
Promise 기능을 사용하였음.

2019년 11월 6일
-------
ㅇ 당연한 얘기이지만 소켓 주소나 포트 정보는 EC2 의 것을 사용하여 별개의 rds 서버 정보와 
겹치지 않는다. 

ㅇ URL 과 세부 정보를 서버 정보에 담아도 상관 없지만, 소켓에서 크게 의미 있는 것은 아님

2019년 11월 7일
------
ㅇ Listview 는 flatList 이 완전히 대체될 예정이니, 주의할 것. / (렌더링 시 사용)

ㅇ 서버, 배포 등 반복 작업에서는 매뉴얼로 관리하자!

2019년 11월 8일
---------
ㅇ mysql 계열 foreign key 연결관계에 대해 엄격한 부분이 있다. 
set foreign_key_checks = 0 이라는 방법이 있지만, 좋지 않은 방법임.

ㅇ of 메소드로 분기된 소켓 io로 설정을 하였을 때, 구성원 모두가 내용이 공유되는 채팅을 위해서 해당 io로 
emit 을 해야 한다.

ㅇ 시퀄라이즈는 Promise 기반으로 비동기를 지원한다. then() 으로 타이밍을 잡아주자!


2019년 11월 9일
--------------
ㅇ 에라토스테네스의 체

ㅇ for 문을 2번 사용하되, 배수를 체크해주는 부분은 전체 범위에 대해 해줌으로써 경우의 수를 크게 줄이는 방법을
사용하도록 하자.

2019년 11월 10일
------------
ㅇ Bash 는 Bourne Again Shell 의 축약어 이며, 리눅스에서 가장 널리 사용되는 쉘임

ㅇ 쉘은 사용자가 커널에 직접 명령을 내릴 수 있게 하는 프로그램이다. 

ㅇ nvm 설치를 통해 node.js 와 npm 

2019년 11월 11일
------------
ㅇ Redux 라이브러리는 3가지 개념이 있다. Store - 모든 states 를 관리한다. Reducer - Store
내부에 존재하며, 새로운 상태를 만드는 함수, Action(주문서)- dispatch 메소드와 같이 쓰이며 어떤 동작을 할 것인지 구체적으로
기술되어 있음

ㅇ Redux 는 상태 예측이 가능하고 유지보수에 유리한 장점을 가지고　있음．

2019년 11월 12일
----------------

ㅇ React app 을 쉽게 개발할 수 있도록 도와주는 도구로 expo 가 있다.
유용한 앱 모듈들이 탑재되어 있음.

ㅇ 그러나, 결제 등 포함안 된 모듈에 대해서 사용하기 위해서는 eject 기능 사용을 통해 native 와 연결시켜주는 것이 필요하다.

2019년 11월 13일
------------

ㅇ android studio 설치하면 sdk 가 따라나옴

ㅇ webview 로 외부 사이트 실행 내용을 가져올 수 있음.

2019년 11월 14일
------------

ㅇ React-Native 와 연계한 안드로이드 에뮬레이터를 띄우기 위해서는 React-native start 가 필요하고,

ㅇ 빌드를 시킨 이후에 npx react-native run-android 를 통해서 에뮬레이터 화면을 확인할 수 있습니다. 

ㅇ npx cli 로 설치된 것은 CRA 프로젝트를 생성 후 다시 패키지를 삭제해서 무거운 패키지를 남기지 않고,
항상 최신 버전의 CRA 를 사용하는 장점이 있다. (npm cli 대비)

2019년 11월 15일
-----------
ㅇ 리덕스에서는 connect 함수를 많이 사용한다. 함수를 받고, 함수를 내주는 형태를 가지고 있다. 대상의 앱(객체, 클래스)이
조금 더 store 에 접근하기 쉽게 연결을 해주는 것이다.

ㅇ state 는 store 안에 있는 것이고, 리듀서 함수(mapStateToProps, mapDispatchToProps)를 통해서 state 및 액션을 받아서
어플리케이션에서 props 로 받아 사용할 수 있게 되는 것.

ㅇ 리덕스 라이브러리를 사용해서 연결시켜주는 것이다. 

2019년 11월 16일
-------------
ㅇ 타입스크립트에서는 new 키워드를 이용해서 생성자의 인터페이스를 정의할 수 있다.

ㅇ 타입스크립트 interface : 클래스에 대한 프로퍼티와 메소드의 타입 만을 선언하는 부분, 구체적인 구현과 정의는 클래스가 담당한다.

2019년 11월 17일
------------
ㅇ 타입스크립트 : 타입만 정해주는 파일인 경우 확장자 .ts / 컴포넌트를 만들어주는 경우 : tsx

ㅇ Redux 핵심규칙 중 하나가 절대 state 를 직접 변경하지 않는 것이기 때문에, Object.assign 등을 사용한다. 

2019년 11월 18일
--------------
ㅇ bind() 메소드를 사용할 때 인자로 함수와 null 값이 들어가서, 영향을 주는 값이 없더라도 결과값으로 나오는 함수는
인자의 함수와는 다르다.

ㅇ git push origin dev --force 는 이전에 올렸던 파일들을 무시하고 업로드가 가능하다.

ㅇ {} 는 JSX 에서 자바스크립트 변수(객체)를 사용할 때 사용하는 문법이다. 

2019년 11월 19일
---------------
ㅇ navigation prop 은 stack navigator 의 모든 screen component 에 전달됨.

ㅇ gradle 파일 빌드를 위해서는 react-native start 의 서버 가동이 필요하다. 

2019년 11월 20일
---------------
ㅇ Bundle 은 클래스다. 여러가지 타입의 값을 저장하는 Map 클래스

ㅇ Android 에서는 Activity 간 데이터를 주고 받을 때 Bundle 클래스를 사용하여 데이터를 전송

ㅇ Bundle 의 다른 용도는 Activity 생성할 때 Bundle savedInstanceState 객체를 가지고 와서
액티비티를 중단할 때 savedInstanceState 메서드를 호출하여 임시적으로 데이터를 저장한다.

2019년 11월 21일
------------
ㅇ 빌드 및 번들 캐시 데이터로 인한 오류 시 조치 방법
- bundle 삭제 
* rm android/app/src/main/assets/index.android.bundle

- bundle 생성
* react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res

- 빌드 관련 gradle 로그 삭제 & 빌드 
* ./gradlew clean && ./gradlew assembleRelease

- 안드로이드 앱 구동
* react-native run-android --variant=release

2019년 11월 22일
----------------

ㅇ Proguard를 활성화하여 APK 의 크기를 줄이는 방법은 android/app/build.gradle에서 enableProguardInReleaseBuilds 를 false(샘플이미지)에서 true로 변경한다.

ㅇ React-native run-android –variant=release 는 서명을 설정한 경우에만 사용할 수 있다.

2019년 11월 23일
---------------

ㅇ  adb devices 현재 에뮬레이터 정보 확인 가능

ㅇ react-native log-android 명령어로 console.log 등의 로그 확인

2019년 11월 24일
-------------

ㅇ 배경 이미지를 지정할 때 ImageBackground 태그 사용

ㅇ 중첩 삼항 연산자 관련해서 조건문 ? A : 조건문 ? B : ... 조건문의 나열으로 Switch case 의 효과를 줄 수 있습니다.

2019년 11월 25일
-----------------
ㅇ 블로깅을 통해 얻는 것보다 공식문서를 더 정확히 보는 연습을 하자.

ㅇ bashrc 설정이 제대로 되어 있지 않았고, init 초기 개발환경도 제대로 잡혀있지 않았음.

2019년 11월 26일
-----------------
ㅇ react native init 으로 새로 프로젝트 생성, 환경변수 재설정, 렌더링 확인

ㅇ fontWeight : 'bold' , native base 이용한 페이지 구성은 편리함.

ㅇ 페이지 제작을 위해서 npm install react-native-table-component 모듈 

2019년 11월 27일
---------------------
ㅇ 알림창 꾸며주는 모듈 $ npm i react-native-awesome-alerts --save

2019년 11월 28일
---------------
ㅇ navigation 모듈 기능에는 header Mode float 을 주고, navigationOptions 를 설정을 통해
헤더를 공통으로 적용할 수 있는 기능이 있다. 

2019년 11월 29일
---------------

ㅇ react native export default 로 하면 괄호 없이 import 할 수 있다.

ㅇ default 없이 export 했을 때, 괄호를 이용해서 import 시켜야 한다. 

ㅇ 두 개 이상의 패키지에서 이름이 겹치는 경우 as 를 사용하면 변수명을 변경할 수 있다. 

2019년 11월 30일
-------------------------

ㅇ navigation 에서 props 를 넘겨주는 방법에는 screenProps 가 존재한다. 

2019년 12월 1일
----------------
ㅇ JSX 문법에서 특수문자를 사용하려면, 엔티티 코드를 사용해야 함.

ㅇ onPress 클릭이벤트와 navigation을 이용해서 페이지를 전환할 때에는 에로우 펑션을 사용한다. 


2019년 12월 2일
----------------
ㅇ navigation 으로 연결하려면, stackNavigator로 묶어주는 것도 중요하지만 자식-부모 구성요소로 연결되어 있는 경우
navigation={this.props.navigation} 으로 전달하는 것이 중요하다.

ㅇ this.state 내에서 정의하고 있는 요소(는 this.state 내에서 미리 사용할 수 없다. 

2019년 12월 3일
---------------
ㅇ react 는 state 원형이 보존되기 때문에 직접 수정할 수 없고, map, filter, concat 등과
setState 를 이용해서 값을 수정할 수 있다.

ㅇ Fetch Get 요청은 default 값이니까, Promise 특성을 이해하고 then 메소드를 이용해서 json() 타입으로 변환하여
데이터에 접근할 수 있다.
