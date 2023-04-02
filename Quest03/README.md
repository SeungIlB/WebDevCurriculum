# Quest 03. 자바스크립트와 DOM

## Introduction
* 자바스크립트는 현재 웹 생태계의 근간인 프로그래밍 언어입니다. 이번 퀘스트에서는 자바스크립트의 기본적인 문법과, 자바스크립트를 통해 브라우저의 실제 DOM 노드를 조작하는 법에 대하여 알아볼 예정입니다.

## Topics
* 자바스크립트의 역사
* 기본 자바스크립트 문법
* DOM API
  * `document` 객체
  * `document.getElementById()`, `document.querySelector()`, `document.querySelectorAll()` 함수들
  * 기타 DOM 조작을 위한 함수와 속성들
* 변수의 스코프
  * `var`, `let`, `const`

## Resources
* [자바스크립트 첫걸음](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps)
* [자바스크립트 구성요소](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Building_blocks)
* [Just JavaScript](https://justjavascript.com/)

## Checklist
* 자바스크립트는 버전별로 어떻게 변화하고 발전해 왔을까요?
  - 자바스크립트는 1995년 넷스케이프 커뮤니케이션즈의 브렌던 아이크(Brendan Eich)가 개발한 프로그래밍 언어로, 초기 버전에서는 단순한 인터랙티브 웹 페이지를 위한 스크립트 언어로 사용되었습니다. 이후 자바스크립트의 기능이 계속해서 확장되면서 다양한 영역에서 활용되고 있습니다.
    - ES1(1997)
    최초의 ECMAScript 표준, 기본 문법과 데이터 타입, 연산자, 함수 등이 정의되어 있습니다.

    - ES2(1998)
    표준화 과정에서 수정된 내용을 반영한 버전입니다.

    - ES3(1999)
    자바스크립트의 표준이 확립된 버전, try-catch 구문, 정규 표현식, switch문 등이 추가되었습니다.

    - ES4(포기됨)
    ECMAScript 4.0이라는 이름으로 발표되었지만, 대규모 확장과 변화를 가져와서 브라우저 벤더들의 지지를 받지 못하고 개발이 중단되었습니다.

    - ES5(2009)
    현재까지 가장 많이 사용되는 버전으로, 엄격 모드(strict mode), JSON 지원, Array 메소드 등이 추가되었습니다.

    - ES6(2015)
    중요한 업데이트로, let, const 키워드, 화살표 함수, 클래스, 모듈 등이 추가되었습니다.

    - ES7(2016)
    Array.prototype.includes() 메소드, 지수 연산자(**) 등이 추가되었습니다.

    - ES8(2017)
    async/await 키워드, Object.values(), Object.entries() 등이 추가되었습니다.

    - ES9(2018)
    Rest/Spread properties, Promise.prototype.finally() 등이 추가되었습니다.

    - ES10(2019)
    Array.prototype.flat(), Array.prototype.flatMap(), String.prototype.trimStart(), String.prototype.trimEnd() 등이 추가되었습니다.

    - 이처럼 ES6부터는 매년 새로운 버전이 발표되고 있으며, 각 버전에서는 기능이 추가되거나 개선되어 JavaScript의 활용 범위가 더욱 넓어지고 있습니다. 최신 버전을 학습하고 적용함으로써 보다 효율적이고 강력한 코드를 작성할 수 있습니다.
  * 자바스크립트의 버전들을 가리키는 ES5, ES6, ES2016, ES2017 등은 무엇을 이야기할까요?
  * 자바스크립트의 표준은 어떻게 제정될까요?
    - 자바스크립트의 표준은 ECMA International이라는 비영리 표준화 기구에서 정의합니다. ECMA International은 정보 통신 기술과 컴퓨터 공학 분야에서 국제적인 표준을 제정하는 데 중점을 둔 기구로, 다양한 기술 표준화를 담당하고 있습니다.
* 자바스크립트의 문법은 다른 언어들과 비교해 어떤 특징이 있을까요?
  * 자바스크립트의 문법은 C, Java, Python 등 다른 프로그래밍 언어들과 많은 부분이 공통적입니다. 그러나 자바스크립트는 함수형 프로그래밍과 프로토타입 기반 객체지향 프로그래밍을 지원하며, 이러한 특징들은 다른 언어들과 차이가 있습니다.

  1. 함수형 프로그래밍 지원
  자바스크립트는 함수가 일급 객체(first-class citizen)이므로, 함수를 변수에 할당하거나 다른 함수의 인자로 전달할 수 있습니다. 이러한 특징은 함수형 프로그래밍에서 중요한 역할을 합니다.

  2. 프로토타입 기반 객체지향 프로그래밍 지원
  자바스크립트는 객체를 생성할 때 클래스(class)가 아닌 프로토타입(prototype)을 사용합니다. 이러한 방식으로 객체를 생성하는 것을 프로토타입 기반 객체지향 프로그래밍(Prototype-based Object-Oriented Programming)이라고 합니다. 이 방식은 클래스 기반 객체지향 프로그래밍(Class-based Object-Oriented Programming)과는 다른 방식으로 객체를 생성하고 관리합니다.

  3. 변수 선언 방식
  자바스크립트는 ES6부터 let과 const라는 블록 스코프 변수를 지원하며, 이전에는 var 키워드로 변수를 선언했습니다. var 변수는 함수 스코프를 가지고 있으며 호이스팅(hoisting)이라는 특징을 가지고 있습니다.

  4. 세미콜론
  자바스크립트는 세미콜론(;)을 사용하여 문장(statement)의 끝을 표시하지만, 이를 생략해도 에러가 발생하지 않습니다. 그러나 생략한 세미콜론이 예기치 않은 에러를 발생시킬 수 있으므로, 일관된 스타일로 세미콜론을 사용하는 것이 좋습니다.

  5. 동적 타이핑
  자바스크립트는 변수의 타입을 런타임 시점에 동적으로 결정합니다. 이러한 동적 타이핑은 코드의 유연성을 높여주지만, 타입 오류 발생 가능성도 높여줍니다. 따라서 코드의 안정성을 위해 타입스크립트(TypeScript)와 같은 정적 타입 검사 기능을 제공하는 도구를 사용하기도 합니다.
  * 자바스크립트에서 반복문을 돌리는 방법은 어떤 것들이 있을까요?
    - JavaScript에서 반복문을 돌리는 방법으로는 크게 4가지가 있습니다.
    - for문: for문은 가장 기본적인 반복문입니다. 반복 횟수를 정확히 알고 있을 때 사용합니다.
    javascript
    ```
    for (초기식; 조건식; 증감식) {
      // 반복 실행될 코드
    }
    ```
    - while문: while문은 조건식이 참인 동안 계속해서 반복됩니다. 반복 횟수가 불확실할 때 사용합니다.
    ```
    javascript
    
    while (조건식) {
      // 반복 실행될 코드
    }
    ```
    - do-while문: do-while문은 while문과 비슷하지만, 조건식을 맨 뒤에 놓습니다. 따라서, do-while문은 조건식이 거짓일 때도 한 번은 실행됩니다.
    ```
    javascript
    
    do {
      // 반복 실행될 코드
    } while (조건식);
    ```
    - for...in문: for...in문은 객체의 속성을 반복해서 처리할 때 사용합니다.
    ```
    javascript
    
    for (변수 in 객체) {
      // 반복 실행될 코드
    }
    ```
    - 여기에 ES6부터 추가된 for...of문도 있습니다. for...of문은 배열의 요소를 반복해서 처리할 때 사용합니다.
    ```
    javascript
    
    for (변수 of 배열) {
      // 반복 실행될 코드
    }
    ```
* 자바스크립트를 통해 DOM 객체에 CSS Class를 주거나 없애려면 어떻게 해야 하나요?
  * JavaScript를 통해 DOM 객체에 CSS Class를 추가하거나 제거하기 위해서는 `classList` 속성을 사용합니다. `classList` 속성은 해당 요소의 클래스를 다루기 위한 메서드(`add`, `remove`, `toggle`, `contains`)를 포함하고 있습니다.

  * CSS Class 추가하기
  ```
  javascript
  
  // 요소에 class 추가
  element.classList.add('class-name');
  ```
  * CSS Class 제거하기
  ```
  javascript
 
  // 요소에서 class 제거
  element.classList.remove('class-name');
  ```
  * CSS Class 토글하기
  ```
  javascript
  
  // 요소의 class가 존재하면 제거하고, 없으면 추가
  element.classList.toggle('class-name');
  ```
  * CSS Class 포함 여부 확인하기
  ```
  javascript
  
  // 요소의 class에 'class-name'이 포함되어 있는지 확인
  if (element.classList.contains('class-name')) {
    // 실행될 코드
  }
  ```
  * 위와 같이 classList 속성을 활용하여 요소에 CSS Class를 추가하거나 제거할 수 있습니다.

  * IE9나 그 이전의 옛날 브라우저들에서는 어떻게 해야 하나요?
    * IE9나 그 이전의 옛날 브라우저들에서는 classList 속성이 지원되지 않습니다. 따라서, className 속성을 사용하여 CSS Class를 추가하거나 제거해야 합니다.

    CSS Class 추가하기
    ```
    javascript
    
    // 요소에 class 추가
    element.className += ' class-name';
    ```
    위의 코드는 요소의 className 속성에 새로운 클래스 이름을 추가합니다. 다만, 이 방법은 클래스 이름이 이미 존재할 경우 중복되어 추가됩니다.

    CSS Class 제거하기
    ```
    javascript
    
    // 요소에서 class 제거
    var removeClass = 'class-name';
    var regex = new RegExp('\\b' + removeClass + '\\b', 'g');
    element.className = element.className.replace(regex, '');
    ```
    위의 코드는 요소의 className 속성에서 특정 클래스 이름을 찾아 제거합니다. RegExp 객체를 사용하여 정규 표현식으로 클래스 이름을 찾고, replace() 메서드를 사용하여 찾은 클래스 이름을 빈 문자열로 대체합니다.

    위와 같이 `className` 속성을 활용하여 요소에 CSS Class를 추가하거나 제거할 수 있습니다. 다만, 이 방법은 클래스 이름이 이미 존재할 경우 중복되어 추가되거나, 정확한 클래스 이름을 찾지 못할 수 있기 때문에 주의해야 합니다. 또한, classList와 달리 토글 기능을 제공하지 않습니다.
* 자바스크립트의 변수가 유효한 범위는 어떻게 결정되나요?
  * 블록 스코프와 함수 스코프가 있음
  * 우리가 아는 대부분의 언어와 비슷함 중괄호 안에 들어갔을 때 대부분 스코프가 정해짐.
  * ES6(ES2015)부터 도입된 `let`과 `const` 키워드를 사용하면 블록 스코프를 만들 수 있습니다. 블록 스코프는 중괄호({})로 감싸진 코드 블록 내에서 선언된 변수가 블록 밖에서는 유효하지 않습니다.
  ```
  {
  let x = 10; // 블록 스코프
  console.log(x); // 10
  }
  console.log(x); // ReferenceError: x is not defined 불가능ㅋㅋ
  ```
  * ES6 이전에는 `var` 키워드를 사용하여 변수를 선언할 때 함수 스코프를 만들 수 있습니다. 함수 스코프는 함수 내에서 선언된 변수가 함수 밖에서는 유효하지 않습니다.
  ```
  function foo() {
  var x = 10; // 함수 스코프
  console.log(x); // 10
  }
  foo();
  console.log(x); // ReferenceError: x is not defined 안됨 ㅋㅋ
  ```
  * 자바스크립트에서는 변수의 유효 범위가 함수나 코드 블록에만 국한되지 않고 전역 스코프(global scope)도 존재합니다. 전역 스코프는 어떤 함수나 코드 블록에도 속하지 않은 최상위 수준의 스코프를 말합니다. 전역 스코프에서 선언된 변수는 어디에서든지 참조할 수 있습니다.
  * `var`과 `let`으로 변수를 정의하는 방법들은 어떻게 다르게 동작하나요?
  * var과 let은 모두 변수를 정의하는 데 사용되는 키워드입니다. 하지만 두 키워드는 동작 방식에 차이가 있습니다.

  * var는 함수 레벨 스코프를 가지며, 변수가 함수 내에서 정의되면 함수 내에서 유효하게 됩니다. 함수 내에서 정의하지 않은 변수는 전역 변수로 선언되며 전역 스코프를 가집니다. var는 변수를 중복 선언할 수 있고, 선언하기 전에 사용할 수 있습니다.

  * let은 블록 레벨 스코프를 가집니다. 변수가 블록 내에서 정의되면 블록 내에서만 유효하며, 블록 밖에서는 사용할 수 없습니다. let은 변수를 중복 선언할 수 없습니다. 또한 변수를 선언하기 전에 사용할 수 없습니다.
* 자바스크립트의 익명 함수는 무엇인가요?
  * 익명 함수(anonymous function)란 이름이 없는 함수를 말합니다. 자바스크립트에서는 함수도 객체이므로 함수를 정의할 때 변수에 함수를 할당할 수 있습니다. 이때 변수에 할당되는 함수가 익명 함수입니다.
  ```
  var greeting = function() {
  console.log('Hello, world!');
  };
  ```
  ```
  setTimeout(function() {
  console.log('Hello, world!');
  }, 1000);
  greeting();
  ```
  * 익명 함수는 주로 콜백 함수(callback function)로 사용됩니다. 콜백 함수는 다른 함수의 인자로 전달되어 실행되는 함수를 말합니다. 이때 콜백 함수로 익명 함수를 사용하면 코드를 간결하게 작성할 수 있습니다. 예를 들어, 다음과 같이 setTimeout() 함수의 인자로 익명 함수를 전달하여 1초 후에 'Hello, world!'를 출력하는 코드를 작성할 수 있습니다.
  * 자바스크립트의 Arrow function은 무엇일까요?
    * Arrow function(화살표 함수)은 ES6(ES2015)에서 추가된 새로운 함수 정의 방법입니다. Arrow function은 `function` 키워드 대신 => 화살표를 사용하여 함수를 정의합니다.
  ```
  // 매개변수가 없는 Arrow function
  () => {
    console.log('Arrow function');
  }

  // 매개변수가 하나인 Arrow function
  x => {
    console.log(x);
  }

  // 매개변수가 여러 개인 Arrow function
  (x, y) => {
    console.log(x + y);
  }

  // 함수 몸체가 한 줄인 Arrow function
  x => console.log(x)

  // 객체를 반환하는 Arrow function
  () => ({ name: 'John', age: 30 })
  ```
  * Arrow function은 코드의 가독성을 높여주고, this 바인딩을 명확하게 해주는 장점이 있습니다. 하지만, 일반 함수와 다르게 arguments 객체를 사용할 수 없으며, 생성자로 사용할 수 없습니다.
  기존의 함수 정의 방식과 다르게 Arrow function은 자신만의 `this`, `arguments`, `super`, `new.target`을 가지지 않습니다. 대신, 외부 스코프의 `this`를 그대로 사용합니다. 이러한 특징 때문에 일반적으로 간단한 함수나 콜백 함수를 작성할 때 많이 사용됩니다.

## Quest
* (Quest 03-1) 초보 프로그래머의 영원한 친구, 별찍기 프로그램입니다.
  * [이 그림](jsStars.png)과 같이, 입력한 숫자만큼 삼각형 모양으로 콘솔에 별을 그리는 퀘스트 입니다.
    * 줄 수를 입력받고 그 줄 수만큼 별을 그리면 됩니다. 위의 그림은 5를 입력받았을 때의 결과입니다.
  * `if`와 `for`와 `function`을 다양하게 써서 프로그래밍 하면 더 좋은 코드가 나올 수 있을까요?
  * 입력은 `prompt()` 함수를 통해 받을 수 있습니다.
  * 출력은 `console.log()` 함수를 통해 할 수 있습니다.
* (Quest 03-2) skeleton 디렉토리에 주어진 HTML을 조작하는 스크립트를 완성해 보세요.
  * 첫째 줄에 있는 사각형의 박스들을 클릭할 때마다 배경색이 노란색↔흰색으로 토글되어야 합니다.
  * 둘째 줄에 있는 사각형의 박스들을 클릭할 때마다 `enabled`라는 이름의 CSS Class가 클릭된 DOM 노드에 추가되거나 제거되어야 합니다.
* 구현에는 여러 가지 방법이 있으나, 다른 곳은 건드리지 않고 TODO 부분만 고치는 방향으로 하시는 것을 권장해 드립니다.

## Advanced
* Quest 03-1의 코드를 더 구조화하고, 중복을 제거하고, 각각의 코드 블록이 한 가지 일을 전문적으로 잘하게 하려면 어떻게 해야 할까요?
* Quest 03-2의 스켈레톤 코드에서 `let` 대신 `var`로 바뀐다면 어떤 식으로 구현할 수 있을까요?
