# Quest 13. 웹 API의 응용과 GraphQL

## Introduction
* 이번 퀘스트에서는 차세대 웹 API의 대세로 각광받고 있는 GraphQL에 대해 알아보겠습니다.

## Topics
* GraphQL
  * Schema
  * Resolver
  * DataLoader
* Apollo

## Resources
* [GraphQL](https://graphql.org/)
* [GraphQL.js](http://graphql.org/graphql-js/)
* [DataLoader](https://github.com/facebook/dataloader)
* [Apollo](https://www.apollographql.com/)

## Checklist
* GraphQL API는 무엇인가요? REST의 어떤 단점을 보완해 주나요?
  * GraphQL API는 클라이언트와 서버 간 데이터 통신을 위한 쿼리 언어로, 페이스북에서 개발한 것입니다. RESTful API와는 다르게, 클라이언트가 필요한 데이터를 명시적으로 요청할 수 있으며, 서버는 해당 요청에 대해서 정확히 필요한 데이터만 응답합니다.

  GraphQL API는 REST의 몇 가지 단점을 보완해줍니다. 첫째, RESTful API에서는 여러 개의 엔드포인트를 호출하여 하나의 기능을 수행해야하는 경우가 있습니다. 이는 요청/응답 대기 시간이 증가하고, 대역폭이 낭비되는 문제를 초래할 수 있습니다. 반면, GraphQL API에서는 클라이언트가 필요한 데이터를 명시적으로 요청할 수 있으므로, 필요한 데이터만 가져오기 때문에 네트워크 자원을 더 효율적으로 사용할 수 있습니다.

  둘째, RESTful API에서는 엔드포인트가 고정되어 있으므로, 서버의 변경이나 업그레이드가 발생하는 경우, 클라이언트 측에서도 해당 엔드포인트에 대한 변경을 수동으로 적용해야합니다. 이는 유지보수 측면에서 부담이 될 수 있습니다. GraphQL API에서는 요청하는 데이터의 구조가 명시적으로 정의되어 있으므로, 서버 측에서 필드를 추가하거나 삭제하는 경우, 클라이언트에서는 자동으로 해당 변경사항을 적용할 수 있습니다.

  마지막으로, RESTful API에서는 과도한 레이어가 발생할 수 있습니다. 예를 들어, 클라이언트에서 여러 개의 엔드포인트를 호출하면서 중복되는 데이터가 발생할 수 있습니다. 이는 데이터의 중복을 초래하며, 응답 시간을 늦출 수 있습니다. GraphQL API에서는 클라이언트에서 필요한 데이터만 요청할 수 있으므로, 중복된 데이터가 발생하지 않고 불필요한 응답 시간도 줄일 수 있습니다.
* GraphQL 스키마는 어떤 역할을 하며 어떤 식으로 정의되나요?
  * GraphQL 스키마는 GraphQL API에서 사용되는 데이터 모델을 정의하는 것으로, API에서 제공하는 모든 객체, 필드, 연결 및 동작을 정의합니다. 스키마는 GraphQL API의 계약서 역할을 하며, 클라이언트와 서버 간에 약속된 데이터 구조를 나타냅니다.

  GraphQL 스키마는 대개 .graphql 파일이나 문자열 형태로 정의됩니다. 스키마는 대개 루트 쿼리, 루트 뮤테이션, 타입 등을 정의합니다. 각각의 타입은 객체, 인터페이스, 열거형 등이 될 수 있으며, 이러한 타입들은 필드와 연결로 구성됩니다. 필드는 타입이 가지는 속성이나 메서드를 정의하며, 연결은 타입 간의 관계를 정의합니다.

  스키마는 GraphQL API의 중심 역할을 합니다. 클라이언트에서 요청하는 데이터가 어떤 형식으로 반환되는지, 어떤 필드와 인자를 사용할 수 있는지, 어떤 연결을 사용할 수 있는지 등을 정의합니다. 또한, 스키마를 기반으로 GraphQL 쿼리가 유효한지 여부를 판단하고, 쿼리를 해석하여 데이터를 가져오는 데 사용됩니다. 따라서 스키마는 GraphQL API의 설계와 개발을 위한 핵심 요소입니다.

* GraphQL 리졸버는 어떤 역할을 하며 어떤 식으로 정의되나요?
  * GraphQL 리졸버는 GraphQL API에서 요청된 데이터를 실제로 처리하는 함수입니다. 즉, 클라이언트가 요청한 쿼리에 해당하는 데이터를 반환하는 로직을 구현하는 역할을 합니다. 리졸버는 스키마의 필드와 연결에 대한 구현을 담당합니다.

  GraphQL 리졸버는 GraphQL API에서 실행될 때 호출되며, 스키마에서 정의된 필드와 인자를 사용하여 데이터를 반환합니다. 리졸버는 필드와 연결 각각에 대해 정의되며, 필드와 연결이 반환하는 데이터 유형에 따라 적절한 리졸버를 선택해야 합니다.

  리졸버는 대개 객체 형태로 정의되며, 해당 객체의 필드와 연결에 대한 로직을 포함합니다. 리졸버는 GraphQL 서버에서 사용하는 언어로 작성될 수 있습니다. 예를 들어, JavaScript로 작성된 GraphQL 서버에서는 리졸버가 JavaScript 함수로 정의될 수 있습니다.

  GraphQL에서 리졸버는 다양한 기능을 수행할 수 있습니다. 예를 들어, 데이터베이스 쿼리를 수행하거나 외부 API와 통신할 수 있습니다. 또한, 리졸버는 데이터 변환, 유효성 검사, 인증 및 권한 부여 등의 기능을 수행할 수 있습니다. 따라서 리졸버는 GraphQL API에서 핵심 역할을 담당하며, API의 성능과 기능을 결정하는 중요한 요소입니다.

  * GraphQL 리졸버의 성능 향상을 위한 DataLoader는 무엇이고 어떻게 쓰나요?
    * DataLoader는 GraphQL 리졸버의 성능 향상을 위해 사용되는 유틸리티 라이브러리입니다. DataLoader는 데이터를 한 번에 로드하고, 캐시하고, 중복 요청을 제거하여 성능을 개선합니다.

    DataLoader를 사용하면 일괄 처리(batching)를 수행하여 데이터를 효율적으로 로드할 수 있습니다. 일괄 처리란 단일 요청에서 여러 데이터를 가져오는 것을 의미합니다. DataLoader는 이러한 일괄 처리를 수행하여 리소스 사용량을 최소화하고 응답 시간을 단축합니다.

    DataLoader는 GraphQL 리졸버에서 다음과 같이 사용됩니다.

    DataLoader 인스턴스 생성: DataLoader는 인스턴스를 생성하여 사용합니다. 인스턴스는 생성자 함수를 사용하여 생성됩니다.

    로드 함수 정의: 리졸버에서 데이터를 로드하는 함수를 정의합니다. 이 함수는 DataLoader 인스턴스를 사용하여 데이터를 로드합니다.

    로드 함수 호출: 리졸버에서 로드 함수를 호출합니다. 이때 DataLoader는 데이터를 일괄 처리하여 반환합니다.

    DataLoader는 중복 요청을 제거하여 성능을 개선하는 데 도움이 됩니다. 예를 들어, 여러 클라이언트가 동일한 데이터를 요청하는 경우 DataLoader는 중복 요청을 제거하고 데이터를 한 번만 로드합니다. 이렇게 하면 리소스 사용량이 감소하고 성능이 향상됩니다.

    DataLoader는 Node.js 및 JavaScript 환경에서 사용할 수 있으며, 다양한 데이터 소스와 연동할 수 있습니다. DataLoader는 GraphQL 리졸버의 성능을 개선하는 강력한 도구이며, GraphQL API의 성능을 향상시키는 데 큰 역할을 합니다.

* 클라이언트 상에서 GraphQL 요청을 보내려면 어떻게 해야 할까요?
  *  클라이언트에서 GraphQL 요청을 보내기 위해서는 다음과 같은 단계를 거쳐야 합니다.

  * GraphQL 클라이언트 라이브러리 선택: GraphQL 클라이언트 라이브러리를 선택합니다. 여러 가지 라이브러리 중에서는 Apollo Client, Relay Modern, urql 등이 있습니다.

  * GraphQL 요청 작성: GraphQL 요청을 작성합니다. 요청은 GraphQL 쿼리 언어로 작성되며, 필요한 데이터를 지정합니다. 요청에는 쿼리(Query), 뮤테이션(Mutation), 구독(Subscription) 등이 있습니다.

  * GraphQL 요청 보내기: 선택한 GraphQL 클라이언트 라이브러리를 사용하여 GraphQL 요청을 보냅니다. 요청은 HTTP POST 요청으로 보내며, 요청 본문에 GraphQL 요청을 포함합니다.

  * 응답 처리: 서버에서 반환한 GraphQL 응답을 클라이언트에서 처리합니다. 응답은 JSON 형식으로 반환되며, GraphQL 클라이언트 라이브러리에서 응답을 처리하여 데이터를 추출합니다.

  GraphQL 클라이언트 라이브러리를 사용하면 GraphQL 요청을 쉽게 작성하고 보낼 수 있습니다. 라이브러리는 요청과 응답 처리를 자동으로 수행하여 개발자가 직접 작성해야 하는 코드 양을 줄여줍니다. 또한, 라이브러리는 캐시 및 상태 관리 등의 기능을 제공하여 개발자가 GraphQL 클라이언트를 구현하는 데 도움을 줍니다.

  * Apollo 프레임워크(서버/클라이언트)의 장점은 무엇일까요?
    * Apollo 프레임워크는 GraphQL을 이용한 서버와 클라이언트 개발을 간편하게 할 수 있는 도구입니다. 다음은 Apollo 프레임워크의 장점들입니다.

    * 간편한 개발 경험: Apollo 프레임워크는 GraphQL 스키마를 작성하고 데이터를 쿼리하는 작업을 간편하게 할 수 있도록 도와줍니다. 클라이언트와 서버 개발 모두에 대한 높은 수준의 추상화를 제공합니다.

    * 자동 캐싱: Apollo 프레임워크는 자동으로 캐싱 기능을 제공하여, 불필요한 네트워크 요청을 줄여 성능을 개선할 수 있습니다.

    * 리액트와의 연동성: Apollo 프레임워크는 리액트와 함께 사용하도록 설계되어 있습니다. 이를 통해, Apollo를 이용하여 리액트 애플리케이션을 더욱 쉽게 개발할 수 있습니다.

    * 편리한 개발 도구: Apollo 프레임워크는 다양한 개발 도구를 제공합니다. 예를 들어, GraphQL Playground를 이용하여 GraphQL API를 시각적으로 확인하고 디버깅할 수 있습니다.

    * 유연성: Apollo 프레임워크는 다양한 환경에서 동작할 수 있습니다. 예를 들어, Node.js, Express, Koa 등 다양한 서버 환경에서 동작할 수 있으며, React, Angular, Vue 등 다양한 클라이언트 환경에서도 동작할 수 있습니다.

    * 다양한 플러그인: Apollo 프레임워크는 다양한 플러그인을 제공하여, 기존의 GraphQL API에 쉽게 Apollo를 적용할 수 있습니다. 예를 들어, Apollo Server, Apollo Client 등의 플러그인을 이용할 수 있습니다.

    따라서 Apollo 프레임워크는 GraphQL을 이용한 서버와 클라이언트 개발을 보다 편리하게 할 수 있는 다양한 장점들을 제공합니다.
  * Apollo Client를 쓰지 않고 Vanilla JavaScript로 GraphQL 요청을 보내려면 어떻게 해야 할까요?
    * Vanilla JavaScript로 GraphQL 요청을 보내려면 fetch API를 사용하여 HTTP POST 요청을 보내고, 요청 바디에 GraphQL 쿼리를 작성해야 합니다.

    GraphQL 쿼리를 작성할 때는 다음과 같은 포맷을 사용해야 합니다.
  ```
    graphql
    Copy code
    query {
      // 쿼리 내용
    }
  ```
    예를 들어, "books" 필드를 가진 GraphQL 쿼리를 작성한다면 다음과 같이 작성할 수 있습니다.
  ```
    graphql
    Copy code
    query {
      books {
        id
        title
        author
      }
    }
  ```
    이제 위의 쿼리를 fetch API를 사용하여 서버에 보내는 코드를 작성해보겠습니다.
  ```
    javascript
    Copy code
    const query = `query {
      books {
        id
        title
        author
      }
    }`;
  

    fetch('/graphql', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ query }),
    })
      .then(response => response.json())
      .then(data => console.log(data));
    ```
    위 코드에서 /graphql은 GraphQL 서버의 엔드포인트 URL입니다. 요청 바디에는 query 필드에 작성한 GraphQL 쿼리를 JSON.stringify() 함수를 이용하여 JSON 문자열로 변환한 것을 전달합니다.

    그리고 요청 헤더에는 Content-Type이 application/json임을 명시합니다. 이를 통해, 서버에서 JSON 형식의 데이터를 받을 것임을 알려줍니다.

    마지막으로, fetch API는 Promise 객체를 반환하므로, 데이터를 받은 후 처리할 로직을 then 함수 내부에 작성합니다.

    이와 같이 fetch API를 이용하여 Vanilla JavaScript로 GraphQL 요청을 보낼 수 있습니다. 단, 이 방법은 Apollo Client와 같은 GraphQL 클라이언트 라이브러리에 비해 상대적으로 복잡하고 가독성이 떨어질 수 있으므로, 필요에 따라 GraphQL 클라이언트 라이브러리를 사용하는 것이 좋습니다.

* GraphQL 기반의 API를 만들 때 에러처리와 HTTP 상태코드 등은 어떻게 하는게 좋을까요?
  * GraphQL 기반의 API를 만들 때 에러처리와 HTTP 상태코드를 다음과 같이 처리하는 것이 좋습니다.

  * 에러 처리
  GraphQL은 일반적인 RESTful API와는 달리 모든 응답이 200 OK 상태코드를 반환합니다. 따라서 GraphQL API에서 발생한 에러는 데이터와 함께 응답됩니다. 이러한 에러를 처리하기 위해서는 GraphQL 스키마에서 errors 필드를 정의하여 반환해야 합니다.
  에러가 발생한 경우 errors 필드에 에러 메시지를 작성하여 반환합니다. 이때, 에러 메시지는 클라이언트가 이해할 수 있는 형태로 작성해야 합니다. 이를 위해, 일반적으로 message 필드와 함께 code 필드를 작성하여 에러를 구분하고, 상세한 에러 정보를 제공합니다.

  * HTTP 상태코드 처리
  GraphQL API에서는 HTTP 상태코드가 일관적으로 200 OK를 반환하기 때문에, 성공 여부를 나타내는 data 필드와 함께 상태코드를 반환해야 합니다.
  일반적으로, 성공한 경우 200 OK 상태코드와 함께 data 필드를 반환하고, 에러가 발생한 경우 400 Bad Request 상태코드와 함께 errors 필드를 반환합니다. 또한, 인증과 같은 예외적인 상황에서는 401 Unauthorized, 403 Forbidden, 404 Not Found 등의 HTTP 상태코드를 반환할 수 있습니다.

  이러한 에러처리와 HTTP 상태코드 처리를 위해서는 GraphQL 미들웨어나 프레임워크를 사용하면 편리합니다. 예를 들어, Apollo Server는 에러처리와 HTTP 상태코드 처리를 자동으로 처리해주기 때문에, 간단하게 설정만으로 처리할 수 있습니다.


## Quest
* 메모장의 서버와 클라이언트 부분을 GraphQL API로 수정해 보세요.

## Advanced
* GraphQL이 아직 제대로 수행하지 못하거나 불가능한 요구사항에는 어떤 것이 있을까요?
* GraphQL의 경쟁자에는 어떤 것이 있을까요?
