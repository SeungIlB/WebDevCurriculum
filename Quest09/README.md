# Quest 09. 서버와 클라이언트의 대화

## Introduction
* 이번 퀘스트에서는 서버와 클라이언트의 연동, 그리고 웹 API의 설계 방법론 중 하나인 REST에 대해 알아보겠습니다.

## Topics
* expressJS, fastify
* AJAX, `XMLHttpRequest`, `fetch()`
* REST, CRUD
* CORS

## Resources
* [Express Framework](http://expressjs.com/)
* [Fastify Framework](https://www.fastify.io/)
* [MDN - Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
* [MDN - XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
* [REST API Tutorial](https://restfulapi.net/)
* [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)
* [MDN - CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

## Checklist
* 비동기 프로그래밍이란 무엇인가요?
  * 비동기 프로그래밍이란 특정 코드의 처리가 완료되기 전, 처리하는 도중에도 아래로 계속 내려가며 수행을 하는 것이다.

  * 콜백을 통해 비동기적 작업을 할 때의 불편한 점은 무엇인가요? 콜백지옥이란 무엇인가요?
    * 가독성이 떨어진다: 콜백을 중첩해서 사용하다 보면 코드가 깊어져서 가독성이 떨어지고, 디버깅이 어려워집니다.

    * 에러 처리가 복잡하다: 비동기 작업을 처리하는 도중 에러가 발생했을 때, 어떤 콜백에서 에러가 발생했는지 찾기 어렵기 때문에 에러 처리가 복잡해집니다.

    * 코드 재사용성이 낮다: 콜백 함수가 중첩되어 있다면, 해당 함수를 다른 곳에서 재사용하기 어렵습니다.
    * 콜백지옥(callback hell)은 콜백 함수가 중첩되어 복잡도가 증가하여 코드를 관리하기 어려운 상황을 말합니다. 이는 콜백을 이용한 비동기 처리에서 발생하는 문제 중 하나입니다. 예를 들어, 서버에서 데이터를 받아와 처리한 후 결과를 출력하는 경우, 데이터를 받아오는 작업과 결과를 출력하는 작업이 비동기적으로 처리되기 때문에, 결과를 출력할 때까지 여러 개의 콜백 함수가 중첩될 수 있습니다. 이러한 중첩된 콜백 함수를 효율적으로 관리하기 위해 Promise나 async/await와 같은 방법이 등장하였습니다.
  
  * 자바스크립트의 Promise는 어떤 객체이고 어떤 일을 하나요?
    * '제작 코드(producing code)'는 원격에서 스크립트를 불러오는 것 같은 시간이 걸리는 일을 합니다. 위 비유에선 '가수’가 제작 코드에 해당합니다.
    * '소비 코드(consuming code)'는 '제작 코드’의 결과를 기다렸다가 이를 소비합니다. 이때 소비 주체(함수)는 여럿이 될 수 있습니다. 위 비유에서 소비 코드는 '팬’입니다.
    * 프라미스(promise) 는 '제작 코드’와 '소비 코드’를 연결해 주는 특별한 자바스크립트 객체입니다. 위 비유에서 프라미스는 '구독 리스트’입니다. '프라미스’는 시간이 얼마나 걸리든 상관없이 약속한 결과를 만들어 내는 '제작 코드’가 준비되었을 때, 모든 소비 코드가 결과를 사용할 수 있도록 해줍니다.

  * 자바스크립트의 `async`와 `await` 키워드는 어떤 역할을 하며 그 정체는 무엇일까요?
    * async와 await는 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법입니다. 기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와주죠.
    * 그럼 문법을 좀 더 정확하게 이해하기 위해서 간단한 async await 코드를 보겠습니다.
    ```
    function fetchItems() {
      return new Promise(function(resolve, reject) {
        var items = [1,2,3];
        resolve(items)
      });
    }

    async function logItems() {
      var resultItems = await fetchItems();
      console.log(resultItems); // [1,2,3]
    }
    ```
    JsCopy
    먼저 fetchItems() 함수는 프로미스 객체를 반환하는 함수입니다. 프로미스는 “자바스크립트 비동기 처리를 위한 객체“라고 배웠었죠. fetchItems() 함수를 실행하면 프로미스가 이행(Resolved)되며 결과 값은 items 배열이 됩니다.

    그리고 이제 logItems() 함수를 보겠습니다. logItems() 함수를 실행하면 fetchItems() 함수의 결과 값인 items 배열이 resultItems 변수에 담깁니다. 따라서, 콘솔에는 [1,2,3]이 출력되죠.

    await를 사용하지 않았다면 데이터를 받아온 시점에 콘솔을 출력할 수 있게 콜백 함수나 .then()등을 사용해야 했을 겁니다. 하지만 async await 문법 덕택에 비동기에 대한 사고를 하지 않아도 되는 것이죠.

    ※참고: 만약 위 코드가 왜 비동기 처리 코드인지 잘 이해가 안 가신다면 fetchItems()를 아래의 함수들로 바꿔서 실행해보셔도 괜찮습니다 :)
    ```
    // HTTP 통신 동작을 모방한 코드
    function fetchItems() {
      return new Promise(function(resolve, reject) {
        setTimeout(function() {
          var items = [1,2,3];
          resolve(items)
        }, 3000);
      });
    }

    // jQuery ajax 코드
    function fetchItems() {
      return new Promise(function(resolve, reject) {
        $.ajax('domain.com/items', function(response) {
          resolve(response);
        });
      });
    }
    ```
    JsCopy
    async & await 실용 예제
    async & await 문법이 가장 빛을 발하는 순간은 여러 개의 비동기 처리 코드를 다룰 때입니다. 아래와 같이 각각 사용자와 할 일 목록을 받아오는 HTTP 통신 코드가 있다고 하겠습니다.
    ```
    function fetchUser() {
      var url = 'https://jsonplaceholder.typicode.com/users/1'
      return fetch(url).then(function(response) {
        return response.json();
      });
    }

    function fetchTodo() {
      var url = 'https://jsonplaceholder.typicode.com/todos/1';
      return fetch(url).then(function(response) {
        return response.json();
      });
    }
    ```
    JsCopy
    위 함수들을 실행하면 각각 사용자 정보와 할 일 정보가 담긴 프로미스 객체가 반환됩니다.

    자 이제 이 두 함수를 이용하여 할 일 제목을 출력해보겠습니다. 살펴볼 예제 코드의 로직은 아래와 같습니다.

    fetchUser()를 이용하여 사용자 정보 호출
    받아온 사용자 아이디가 1이면 할 일 정보 호출
    받아온 할 일 정보의 제목을 콘솔에 출력
    그럼 코드를 보겠습니다.
    ```
    async function logTodoTitle() {
      var user = await fetchUser();
      if (user.id === 1) {
        var todo = await fetchTodo();
        console.log(todo.title); // delectus aut autem
      }
    }
    ```
    JsCopy
    logTodoTitle()를 실행하면 콘솔에 delectus aut autem가 출력될 것입니다. 위 비동기 처리 코드를 만약 콜백이나 프로미스로 했다면 훨씬 더 코드가 길어졌을 것이고 인덴팅 뿐만 아니라 가독성도 좋지 않았을 겁니다. 이처럼 async await 문법을 이용하면 기존의 비동기 처리 코드 방식으로 사고하지 않아도 되는 장점이 생깁니다.

    ※참고: 위 함수에서 사용한 fetch() API는 크롬과 같은 최신 브라우저에서만 동작합니다. 브라우저 지원 여부는 다음 링크로 확인해보세요. fetch API 브라우저 지원표

    async & await 예외 처리
    async & await에서 예외를 처리하는 방법은 바로 try catch입니다. 프로미스에서 에러 처리를 위해 .catch()를 사용했던 것처럼 async에서는 catch {} 를 사용하시면 됩니다.

    조금 전 코드에 바로 try catch 문법을 적용해보겠습니다.
    ```
    async function logTodoTitle() {
      try {
        var user = await fetchUser();
        if (user.id === 1) {
          var todo = await fetchTodo();
          console.log(todo.title); // delectus aut autem
        }
      } catch (error) {
        console.log(error);
      }
    }
    ```
    JsCopy
    위의 코드를 실행하다가 발생한 네트워크 통신 오류뿐만 아니라 간단한 타입 오류 등의 일반적인 오류까지도 catch로 잡아낼 수 있습니다. 발견된 에러는 error 객체에 담기기 때문에 에러의 유형에 맞게 에러 코드를 처리해주시면 됩니다.

* 브라우저 내 스크립트에서 외부 리소스를 가져오려면 어떻게 해야 할까요?
  * 브라우저에서 외부 리소스를 가져오기 위해서는 일반적으로 XMLHttpRequest 객체나 fetch API를 사용하여 AJAX 요청을 보내면 됩니다.

  예를 들어, XMLHttpRequest 객체를 사용하여 외부 리소스를 가져오는 방법은 다음과 같습니다.
  ```
  javascript
  Copy code
  const xhr = new XMLHttpRequest();
  xhr.open('GET', 'http://example.com/myfile.txt');
  xhr.onload = function() {
    if (xhr.status === 200) {
      console.log(xhr.responseText);
    }
    else {
      console.log('Request failed.  Returned status of ' + xhr.status);
    }
  };
  xhr.send();
  ```
  이 코드는 외부 리소스인 'http://example.com/myfile.txt'에서 텍스트 파일을 가져와서 콘솔에 로그를 출력합니다. xhr.open() 메서드는 HTTP 요청을 초기화하고, xhr.send() 메서드는 요청을 보냅니다. xhr.onload() 콜백 함수는 요청이 완료되면 실행되며, xhr.status를 통해 HTTP 상태 코드를 확인할 수 있습니다.

  fetch API를 사용하여 외부 리소스를 가져오는 방법은 다음과 같습니다.
  ```
  javascript
  Copy code
  fetch('http://example.com/myfile.txt')
    .then(response => response.text())
    .then(data => console.log(data))
    .catch(error => console.error(error));
  ```
  이 코드는 http://example.com/myfile.txt에서 텍스트 파일을 가져와서 콘솔에 로그를 출력합니다. fetch() 함수는 Promise 객체를 반환하며, then() 메서드를 사용하여 응답 데이터를 처리할 수 있습니다. catch() 메서드는 요청이 실패한 경우 실행됩니다.
  * 브라우저의 `XMLHttpRequest` 객체는 무엇이고 어떻게 동작하나요?
    * XMLHttpRequest는 브라우저에서 HTTP 요청을 보내고 응답을 받을 수 있는 객체입니다. 이를 통해 비동기적으로 서버와 통신하여 웹 페이지를 업데이트하거나 데이터를 가져올 수 있습니다.

    XMLHttpRequest 객체를 생성하려면 먼저 new XMLHttpRequest() 문을 사용합니다. 그런 다음 open() 메소드를 호출하여 요청을 준비하고 send() 메소드를 호출하여 요청을 서버로 보냅니다. 요청에 대한 응답을 받으면 onload 이벤트 핸들러를 사용하여 처리할 수 있습니다.

    예를 들어, 다음은 XMLHttpRequest를 사용하여 서버에서 데이터를 가져오는 간단한 예제입니다:
    ```
    javascript
    Copy code
    const xhr = new XMLHttpRequest();
    xhr.open('GET', '/data', true);
    xhr.onload = function() {
      if (xhr.status === 200) {
        console.log(xhr.responseText);
      } else {
        console.error('Request failed.  Returned status of ' + xhr.status);
      }
    };
    xhr.send();
    ```
    이 예제에서 open() 메소드는 GET 요청을 보내기 위해 '/data' URL을 엽니다. onload 핸들러는 요청이 완료되면 호출되며, status 코드가 200이면 responseText 속성을 사용하여 서버 응답을 콘솔에 로그합니다. 그렇지 않으면 오류 메시지를 출력합니다.

  * `fetch` API는 무엇이고 어떻게 동작하나요?
    * fetch API는 브라우저에서 제공하는 JavaScript API 중 하나로, 네트워크를 통해 리소스를 가져오기 위한 강력한 방법입니다.

    fetch 메소드를 사용하면 서버에서 데이터를 가져오거나, 데이터를 서버로 전송할 수 있습니다. 이 메소드는 Promise를 반환하며, 비동기적으로 작동합니다. Promise는 HTTP 요청의 성공 여부와 관계없이 항상 결과를 반환합니다.

    아래는 fetch API를 사용한 GET 요청의 예시입니다:
    ```
    javascript
    Copy code
    fetch('https://example.com/data.json')
      .then(response => response.json())
      .then(data => console.log(data))
      .catch(error => console.error(error));
    ```
    이 예시에서 fetch 메소드는 https://example.com/data.json URL에 GET 요청을 보내고, response 객체를 반환합니다. response 객체는 json 메소드를 호출하여 JSON 형태의 데이터를 가져오고, then 메소드를 사용하여 가져온 데이터를 콘솔에 출력합니다. 만약 에러가 발생하면 catch 메소드에서 에러를 처리합니다.

    fetch API는 또한 POST, PUT, DELETE 등의 HTTP 메소드를 지원하며, 더욱 강력한 요청을 만들기 위해 옵션 객체를 제공합니다.

* REST는 무엇인가요?
  * REST란 Representational State Transfer의 약어로, 웹 애플리케이션에서 자원(resource)을 정의하고 자원에 대한 주소를 지정하는 방법 중 하나입니다. REST는 HTTP 프로토콜을 기반으로 하며, 클라이언트와 서버 간의 통신에서 자원을 정의하고 자원의 상태를 주고 받기 위한 아키텍처입니다.

  REST는 자원을 URI(Uniform Resource Identifier)로 표현하며, HTTP 메서드(GET, POST, PUT, DELETE 등)를 이용하여 자원에 대한 행위를 표현합니다. 예를 들어, /users/1은 사용자 자원의 URI를 나타내고, GET 메서드를 사용하여 해당 사용자 정보를 가져올 수 있습니다.

  REST는 또한 클라이언트와 서버 간에 데이터를 전송하기 위해 JSON, XML 등의 데이터 형식을 사용합니다. 이를 통해 서버와 클라이언트 간에 자원에 대한 상태를 주고받을 수 있습니다.

  REST는 단순하고 확장성이 높은 아키텍처로 인해, 현재 대부분의 웹 서비스에서 사용되고 있습니다.

  * REST API는 어떤 목적을 달성하기 위해 나왔고 어떤 장점을 가지고 있나요?
    * REST API는 Representational State Transfer(REST) 아키텍처를 따르는 API로, 웹 서비스에서 자원을 정의하고 자원에 대한 주소를 지정하며, HTTP 프로토콜을 사용하여 자원의 상태를 주고받는 것을 목적으로 합니다.

  REST API는 다음과 같은 장점을 가지고 있습니다.

  * 단순성: REST API는 HTTP 프로토콜을 사용하므로, 구현이 간단하고 쉽게 이해할 수 있습니다.

  * 확장성: REST API는 자원을 URI로 표현하며, HTTP 메서드를 사용하여 자원에 대한 행위를 표현하므로, 새로운 자원이나 행위를 추가하기가 용이합니다.

  * 유연성: REST API는 다양한 클라이언트에서 사용할 수 있으며, 서버와 클라이언트 간에 데이터 형식이 일치하지 않더라도 자원에 대한 상태를 주고받을 수 있습니다.

  * 가시성: REST API는 자원에 대한 URI가 명확하게 정의되어 있기 때문에, 자원의 상태를 파악하기 쉽습니다.

  * 성능: REST API는 HTTP 프로토콜을 기반으로 하므로, 캐싱이나 로드 밸런싱 등의 기술을 이용하여 성능을 최적화할 수 있습니다.

  * 보안성: REST API는 HTTPS 프로토콜을 사용하여 통신하므로, 데이터의 안전성을 보장할 수 있습니다.

  따라서, REST API는 단순하면서도 확장성이 높은 아키텍처로, 현재 많은 웹 서비스에서 사용되고 있습니다.

  * RESTful한 API 설계의 단점은 무엇인가요?
    * RESTful한 API 설계의 단점은 다음과 같습니다.

    * 복잡성: RESTful한 API를 설계할 때, 자원의 URI와 HTTP 메서드를 정의하는 것이 중요합니다. 이를 제대로 설계하지 않으면 복잡한 API를 만들게 되어 유지보수와 확장성이 떨어질 수 있습니다.

    * 캐싱의 한계: RESTful한 API에서는 캐시를 이용하여 성능을 최적화할 수 있습니다. 하지만, 캐시 제어를 제대로 처리하지 않으면 캐시가 동기화되지 않아 일관성이 없는 응답이 발생할 수 있습니다.

    * 보안 문제: RESTful한 API에서는 HTTPS를 사용하여 통신하므로 데이터의 안전성을 보장할 수 있습니다. 하지만, API의 자원에 대한 권한을 관리하기 어렵기 때문에, 보안 문제가 발생할 수 있습니다.

    * 과도한 데이터 전송: RESTful한 API에서는 클라이언트와 서버 간의 데이터 전송에 JSON, XML 등의 데이터 형식을 사용합니다. 하지만, 클라이언트와 서버 간에 데이터 형식이 일치하지 않을 경우, 과도한 데이터 전송으로 인해 성능이 저하될 수 있습니다.

    * 한계된 기능: RESTful한 API는 HTTP 메서드를 사용하여 자원에 대한 CRUD(Create, Read, Update, Delete) 작업을 처리합니다. 따라서, 자원에 대한 복잡한 작업이 필요한 경우에는 다른 기술을 결합하여 사용해야 합니다.

    이러한 단점들은 RESTful한 API를 설계할 때 고려해야 할 요소들입니다. 따라서, API를 설계할 때는 단순하고 명확하면서도 유연성과 확장성을 고려하여야 합니다.
* CORS란 무엇인가요? 이러한 기능이 왜 필요할까요? CORS는 어떻게 구현될까요?
  * CORS(Cross-Origin Resource Sharing)는 웹 브라우저에서 발생하는 보안 정책으로, 다른 도메인의 리소스에 접근할 때 발생하는 보안 문제를 해결하기 위해 등장한 기술입니다.

  CORS 기능이 필요한 이유는, 웹 보안 정책 중 하나인 Same-Origin Policy(SOP) 때문입니다. SOP는 웹 애플리케이션에서 다른 출처의 리소스에 접근하는 것을 제한하는 보안 정책입니다. 예를 들어, 도메인 A에서 로드된 스크립트가 도메인 B의 데이터에 접근하는 것을 SOP가 막아서 보안이 강화됩니다. 하지만, SOP는 다른 출처에서의 리소스를 필요로 하는 웹 애플리케이션에 대해서는 제한적입니다.

  CORS는 이러한 SOP의 제한을 느슨하게 만들어 다른 출처의 리소스에 접근할 수 있게 합니다. 서버는 클라이언트의 요청 헤더에 Origin 값을 포함하여 응답하고, 브라우저는 이를 확인하여 동일한 출처의 요청인지 아니면 다른 출처의 요청인지를 판별합니다. 만약 다른 출처의 요청이라면, 브라우저는 서버의 응답 헤더에 Access-Control-Allow-Origin을 확인하여, 해당 출처에서의 요청을 허용할지 말지를 결정합니다.

  CORS를 구현하는 방법은 서버에서 응답 헤더에 Access-Control-Allow-Origin 값을 설정하는 것입니다. 이 값을 "*"로 설정하면 모든 출처에서의 요청을 허용할 수 있고, 특정 출처에서의 요청만을 허용하려면 해당 출처의 주소를 설정하면 됩니다. 또한, HTTP 메서드나 헤더 등을 추가로 허용하려면 Access-Control-Allow-Methods, Access-Control-Allow-Headers 등의 값을 설정할 수 있습니다.


## Quest
* 이번 퀘스트는 Midterm에 해당하는 과제입니다. 분량이 제법 많으니 한 번 기능별로 세부 일정을 정해 보고, 과제 완수 후에 그 일정이 얼마나 지켜졌는지 스스로 한 번 돌아보세요.
  * 이번 퀘스트부터는 skeleton을 제공하지 않습니다!
* Quest 05에서 만든 메모장 시스템을 서버와 연동하는 어플리케이션으로 만들어 보겠습니다.
  * 클라이언트는 `fetch` API를 통해 서버와 통신합니다.
  * 서버는 8000번 포트에 REST API를 엔드포인트로 제공하여, 클라이언트의 요청에 응답합니다.
  * 클라이언트로부터 온 새 파일 저장, 삭제, 다른 이름으로 저장 등의 요청을 받아 서버의 로컬 파일시스템을 통해 저장되어야 합니다.
    * 서버에 어떤 식으로 저장하는 것이 좋을까요?
  * API 서버 외에, 클라이언트를 띄우기 위한 서버가 3000번 포트로 따로 떠서 API 서버와 서로 통신할 수 있어야 합니다.
  * Express나 Fastify 등의 프레임워크를 사용해도 무방합니다.
* 클라이언트 프로젝트와 서버 프로젝트 모두 `npm i`만으로 디펜던시를 설치하고 바로 실행될 수 있게 제출되어야 합니다.
* 이번 퀘스트부터는 앞의 퀘스트의 결과물에 의존적인 경우가 많습니다. 제출 폴더를 직접 만들어 제출해 보세요!

## Advanced
* `fetch` API는 구현할 수 없지만 `XMLHttpRequest`로는 구현할 수 있는 기능이 있을까요?
* REST 이전에는 HTTP API에 어떤 패러다임들이 있었을까요? REST의 대안으로는 어떤 것들이 제시되고 있을까요?
