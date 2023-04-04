# Quest 07. node.js의 기초

## Introduction
* 이번 퀘스트에서는 node.js의 기본적인 구조와 개념에 대해 알아 보겠습니다.

## Topics
* node.js
* npm
* CommonJS와 ES Modules

## Resources
* [About node.js](https://nodejs.org/ko/about/)
* [Node.js의 아키텍쳐](https://edu.goorm.io/learn/lecture/557/%ED%95%9C-%EB%88%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-node-js/lesson/174356/node-js%EC%9D%98-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90)
* [npm](https://docs.npmjs.com/about-npm)
* [npm CLI commands](https://docs.npmjs.com/cli/v7/commands)
* [npm - package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
* [How NodeJS Require works!](https://www.thirdrocktechkno.com/blog/how-nodejs-require-works)
* [MDN - JavaScript Modules](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)
* [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
* [require vs import](https://www.geeksforgeeks.org/difference-between-node-js-require-and-es6-import-and-export/)

## Checklist
* node.js는 무엇인가요? node.js의 내부는 어떻게 구성되어 있을까요?
  ```
  * Node.js는 Chrome V8 JavaScript 엔진을 기반으로 하는 서버 사이드 JavaScript 런타임입니다. Node.js는 이벤트 기반, 비동기 I/O 모델을 사용하여 높은 처리 성능과 확장성을 가지고 있어 서버 사이드 애플리케이션 개발에 많이 사용됩니다.

  Node.js는 모듈 시스템, 파일 시스템, 네트워크, 데이터베이스 등 다양한 기능을 제공합니다. Node.js는 모듈 시스템을 통해 간단한 모듈화를 지원하고 있어 코드의 재사용성이 높습니다. 또한, Node.js는 이벤트 기반 모델을 사용하여 비동기 I/O 처리를 지원합니다. 이를 통해 많은 양의 요청을 처리하면서도 블로킹이 발생하지 않아 애플리케이션의 응답성이 높아지는 장점이 있습니다.

  Node.js의 내부는 크게 두 가지 요소로 구성됩니다. 첫 번째 요소는 Node.js 바인딩입니다. Node.js 바인딩은 V8 JavaScript 엔진과 Node.js API 사이에서 상호 작용하는 레이어입니다. Node.js 바인딩은 C/C++로 작성되어 있으며, V8 JavaScript 엔진과 Node.js API를 상호 연결해주는 역할을 합니다.

  두 번째 요소는 Node.js API입니다. Node.js API는 모듈 시스템, 파일 시스템, 네트워크, 데이터베이스 등 다양한 기능을 제공합니다. Node.js API는 JavaScript로 작성되어 있으며, 이를 사용하여 Node.js 애플리케이션을 개발할 수 있습니다. Node.js API는 비동기 I/O 모델을 사용하여 I/O 작업을 처리하고, 이벤트 기반 모델을 사용하여 이벤트를 처리합니다.

  Node.js의 내부는 크게 V8 JavaScript 엔진, Node.js 바인딩, Node.js API로 구성되어 있습니다. 이러한 요소들이 함께 동작하여 높은 처리 성능과 확장성을 가진 서버 사이드 애플리케이션을 개발할 수 있게 해줍니다.
  ```
* npm이 무엇인가요? `package.json` 파일은 어떤 필드들로 구성되어 있나요?
  ```
  * npm : Node.js 생태계의 패키지 매니저
  (macOS의 패키지 매니저가 brew이듯, node.js 생태계에서 패키지 매니저는 npm이다.)

  Node.js 환경에서 외부 라이브러리를 다운로드 하기 위한 방법들 중 하나이다.
  필요한 모듈을 다운로드 할 수 있는 모듈 스토어로, 앞으로 필요한 모듈의 대부분은 npm에서 다운로드해서 사용하면 된다.
  * `package.json` : 이 프로그램을 실행시키기 위해 필요한 모듈들이 무엇인지, 프로그램을 실행시키는 방법, 프로그램을 테스트하는 방법 등이 명시되어 있다.
  `package.json`에서 필요하다고 하는 모듈들은 npm을 이용해 다운로드 하면 된다.
  npm install 명령어로 모듈들의 다운로드가 완료되면 node.modules 라는 폴더가 생성되는 것을 확인할 수 있다.
  이때, 프로그램을 실행시키기 위해 필요한 실제 모듈은 node.modules라는 폴더에 저장되고, package.json은 어떤 모듈이 들어가 있는지만 적혀있다.
  ```
* npx는 어떤 명령인가요? npm 패키지를 `-g` 옵션을 통해 글로벌로 저장하는 것과 그렇지 않은 것은 어떻게 다른가요?
  ```
  * npx : 새로운 패키지 관리 모듈이 아니라 js 패키지관리 모듈인 npm의 5.2.0 버전 부터 새로 추가 된 도구 npm을 좀 더 편하게 사용하기 위해 npm에서 제공해주는 하나의 도구임.
  npm 패키지를 `-g` 옵션을 통해 글로벌로 설치하는 것과 그렇지 않은 것은 다음과 같은 차이점이 있습니다.

  글로벌로 설치된 패키지는 모든 프로젝트에서 사용할 수 있습니다. 이는 컴퓨터 전체에서 패키지를 공유하게 됨을 의미합니다. 반면 로컬에 설치된 패키지는 해당 프로젝트에서만 사용할 수 있습니다.

  글로벌로 설치된 패키지는 시스템의 경로(PATH)에 추가됩니다. 따라서 글로벌 패키지를 사용하는 경우, 프로젝트에 해당 패키지를 의존성으로 추가할 필요가 없습니다. 반면 로컬 패키지는 프로젝트 내에서 패키지를 설치해야합니다.

  글로벌로 설치된 패키지는 일반적으로 시스템 전체에서 공유하는 라이브러리와 같은 역할을 합니다. 따라서 글로벌 패키지를 설치하려면 일반적으로 관리자 권한이 필요합니다. 반면 로컬 패키지는 일반 사용자 권한으로 설치 가능합니다.

  따라서, 패키지를 글로벌로 설치할지 로컬에 설치할지는 패키지를 사용하는 방식에 따라 결정됩니다. 일회성으로 사용하는 경우에는 npx를 사용하여 패키지를 실행하는 것이 더 효율적이며, 프로젝트에서만 사용하는 패키지는 로컬에 설치하는 것이 좋습니다.
  ```
* 자바스크립트 코드에서 다른 파일의 코드를 부르는 시도들은 지금까지 어떤 것이 있었을까요? CommonJS 대신 ES Modules가 등장한 이유는 무엇일까요?
  ```
  - CommonJS, ESModules를 제외하고도 HTML에서의 script, AMD, UMD 등이 있었다.
	- HTML에서 script를 통해 여러개의 js를 불러오면 전역으로 정의되면서 같은 함수명이나 변수명을 가진 것들이 재정의가 되면서 오염되는 현상이 있었고 +
	- 브라우저 외부에서도 JS를 돌릴 수 있는 구글의 V8이 등장하면서 서버사이드에도 JS를 이용하자는 아이디어가 떠오르면서 +
	- 모듈화의 필요성이 제기되기 시작하였다. (그로인해, CommonJS, AMD, UMD등 등장)
	
  - commonJS(AMD, UMD 포함)는 JS를 브라우저 뿐 아니라 server-side/desktop application에서도 사용할 수 있도록 하는 것이었다.
  - 여러개의 단체에서 각각 모듈을 만든 것은, 결국 그들의 철학이 충돌했기 때문인데, 결국 JS언어 자체에서 module system을 지원해야한다는 목소리가 커지며
  - ES6에서 ESmodule을 직접 지원하기 시작했다.
  ```
* ES Modules는 기존의 `require()`와 동작상에 어떤 차이가 있을까요? CommonJS는 할 수 있으나 ES Modules가 할 수 없는 일에는 어떤 것이 있을까요?
  ```
  - commonJS는 동적으로, ESM은 정적으로 작동한다.
	- 그렇기 때문에, commonJS는 if(~) require(~);가 가능하지만 ESM은 가능하지 않다.
		- 미리 종속성 그래프(dependencies graph)를 그리지 않고 필요한 순간에 가져다 쓰는 방식.
			- 여기에서, 순환참조에 대한 한계점이 드러난다.
			- 당연히 CommonJS는 tree shaking에도 약할 수 밖에 없다.
	- ESM은 정적으로 작동 (즉, 종속성 그래프를 모두 그려놓고 시작하기에, 순환참조를 극복.)

  - call by value vs reference
	  - CommonJS는 call by value 방식, ESM은 call by reference 방식이다.
	  - 그렇기 때문에 이미 파일을 불러온 후에, 원본파일에서 비동기처리로 값이 바뀌면, ESM은 이를 인식하고, CommonJS는 인식하지 못한다.
		  - 참고로, ESM을 통해 불러오면 CONST 처리가 되어서 import해서는 수정이 불가능하다.
  ```
* node.js에서 ES Modules를 사용하려면 어떻게 해야 할까요? ES Modules 기반의 코드에서 CommonJS 기반의 패키지를 불러오려면 어떻게 해야 할까요? 그 반대는 어떻게 될까요?
  ```
  - nodeJS에서 ES Modules 사용하기
	  - 파일단위: .mjs로 파일 확장자 변경 후 사용
	  - 프로젝트 단위: package.json에 type:module을 적으면, js확장자로도 이용가능
	
  - ESM 기반에서 CommonJS 사용하기
	  - default import로 가능 / 내부적인 메서드는 CJS.method1()과 같이 .을 찍어 이용가능
  ```
  
## Quest
* 스켈레톤 코드에는 다음과 같은 네 개의 패키지가 있으며, 용도는 다음과 같습니다:
  * `cjs-package`: CommonJS 기반의 패키지입니다. 다른 코드가 이 패키지의 함수와 내용을 참조하게 됩니다.
  * `esm-package`: ES Modules 기반의 패키지입니다. 다른 코드가 이 패키지의 함수와 내용을 참조하게 됩니다.
  * `cjs-my-project`: `cjs-package`와 `esm-package`에 모두 의존하는, CommonJS 기반의 프로젝트입니다.
  * `esm-my-project`: `cjs-package`와 `esm-package`에 모두 의존하는, ES Modules 기반의 프로젝트입니다.
* 각각의 패키지의 `package.json`과 `index.js` 또는 `index.mjs` 파일을 수정하여, 각각의 `*-my-project`들이 `*-package`에 노출된 함수와 클래스를 활용할 수 있도록 만들어 보세요.

## Advanced
* node.js 외의 자바스크립트 런타임에는 어떤 것이 있을까요?
