# Quest 05. OOP 특훈

## Introduction
* 이번 퀘스트에서는 바닐라 자바스크립트의 객체지향 프로그래밍을 조금 더 훈련해 보겠습니다.

## Topics
* Separation of Concerns
* 객체지향의 설계 원칙
  * SOLID 원칙
* Local Storage

## Resources
* [Separation of concerns](https://jonbellah.com/articles/separation-of-concerns/)
* [SOLID](https://en.wikipedia.org/wiki/SOLID)
* [객체지향 설계 5원칙](https://webdoli.tistory.com/210)
* [MDN - Local Storage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)

## Checklist
* 관심사의 분리 원칙이란 무엇인가요? 웹에서는 이러한 원칙이 어떻게 적용되나요?
  * 관심사의 분리(Separation of Concerns) 원칙은 소프트웨어 공학에서 중요한 원칙 중 하나로, 소프트웨어의 구성 요소를 역할에 따라 분리하여 개발하고 유지보수하는 것을 지향합니다. 이를 통해 각 구성 요소가 자신의 역할에만 집중하고, 다른 역할에 대한 지식과 의존성을 최소화하여 시스템을 보다 쉽게 관리할 수 있습니다.

  웹에서 관심사의 분리 원칙은 대표적으로 Model-View-Controller (MVC) 패턴, Model-View-ViewModel (MVVM) 패턴, Model-View-Presenter (MVP) 패턴 등을 이용하여 구현됩니다. 이러한 패턴들은 각각 모델, 뷰, 컨트롤러, 뷰모델, 프리젠터 등의 역할로 분리하여 개발하고, 각 역할이 자신의 역할에 집중하면서도 다른 역할과의 의존성을 최소화하여 시스템을 보다 쉽게 관리할 수 있습니다.

  예를 들어, MVC 패턴에서는 모델(Model)은 데이터와 비즈니스 로직을 담당하고, 뷰(View)는 사용자 인터페이스(UI)를 담당하며, 컨트롤러(Controller)는 모델과 뷰를 연결하여 사용자의 입력을 처리하고 데이터를 업데이트하는 역할을 담당합니다. 이렇게 역할에 따라 분리된 구성 요소들은 서로 독립적으로 개발될 수 있으며, 다른 구성 요소와의 의존성을 최소화하여 유지보수성을 향상시킬 수 있습니다.

  웹에서 관심사의 분리 원칙은 프론트엔드와 백엔드 모두에 적용됩니다. 프론트엔드에서는 HTML, CSS, JavaScript 등의 역할에 따라 파일을 분리하여 개발하고, 백엔드에서는 데이터베이스, 비즈니스 로직, 라우팅 등의 역할에 따라 코드를 분리하여 개발합니다. 이를 통해 웹 애플리케이션을 보다 쉽게 유지보수하고 확장할 수 있습니다.
* 객체지향의 SOLID 원칙이란 무엇인가요? 이 원칙을 구체적인 예를 들어 설명할 수 있나요?
  * SOLID 원칙은 객체지향 설계의 다섯 가지 기본 원칙으로, 소프트웨어 설계의 유연성, 확장성, 유지보수성, 재사용성 등을 보장하기 위해 만들어졌습니다.

  * 단일 책임 원칙 (Single Responsibility Principle, SRP)
  하나의 클래스는 하나의 책임만 가져야 하며, 클래스가 제공하는 모든 서비스는 그 책임을 수행하는 데 집중되어야 합니다. 예를 들어, 자동차 클래스는 운전, 시동, 정지 등 자동차의 모든 기능을 포함하지 않고, 운전에 대한 기능만 담당해야 합니다.
  ```
  // bad
  class User {
    constructor(name, email) {
      this.name = name;
      this.email = email;
    }

    getName() {
      return this.name;
    }

    getEmail() {
      return this.email;
    }

    sendEmail(subject, message) {
      // send email
    }
  }
  ```
  ```
  // good
  class User {
    constructor(name, email) {
      this.name = name;
      this.email = email;
    }

    getName() {
      return this.name;
    }

    getEmail() {
      return this.email;
    }
  }

  class EmailService {
    sendEmail(user, subject, message) {
      // send email
    }
  }
  ```
  위 코드에서 User 클래스가 사용자 정보를 가지고 있으면서 동시에 이메일을 보내는 역할까지 수행하고 있습니다. 이는 클래스의 책임이 너무 많아져서 SRP 원칙에 위배됩니다. 이를 해결하기 위해 User 클래스는 사용자 정보만을 가지고, 이메일 전송은 EmailService 클래스에서 담당하도록 분리하였습니다.
  * 개방-폐쇄 원칙 (Open-Closed Principle, OCP)
  소프트웨어 개체(클래스, 모듈, 함수 등)는 확장에는 열려 있어야 하지만 변경에는 닫혀 있어야 합니다. 즉, 새로운 기능을 추가할 때는 기존 코드를 수정하지 않고 확장해야 합니다.
  ```
  // bad
  class Rectangle {
    constructor(width, height) {
      this.width = width;
      this.height = height;
    }

    getWidth() {
      return this.width;
    }

    getHeight() {
      return this.height;
    }
  }

  class AreaCalculator {
    constructor(shapes) {
      this.shapes = shapes;
    }

    getTotalArea() {
      let totalArea = 0;
      this.shapes.forEach(shape => {
        if (shape instanceof Rectangle) {
          totalArea += shape.getWidth() * shape.getHeight();
        } else if (shape instanceof Circle) {
          totalArea += Math.PI * shape.getRadius() ** 2;
        }
      });
      return totalArea;
    }
  }
  ```
  ```
  // good
  class Shape {
    getArea() {
      // calculate area
    }
  }

  class Rectangle extends Shape {
    constructor(width, height) {
      super();
      this.width = width;
      this.height = height;
    }

    getArea() {
      return this.width * this.height;
    }
  }

  class Circle extends Shape {
    constructor(radius) {
      super();
      this.radius = radius;
    }

    getArea() {
      return Math.PI * this.radius ** 2;
    }
  }

  class AreaCalculator {
    constructor(shapes) {
      this.shapes = shapes;
    }

    getTotalArea() {
      let totalArea = 0;
      this.shapes.forEach(shape => {
        totalArea += shape.getArea();
      });
      return totalArea;
    }
  }
  ```

  위 코드에서 AreaCalculator 클래스가 도형의 종류에 따라 계산 방식을 다르게 구현하고 있습니다. 이는 OCP 원칙에 위배됩니다. 이를 해결하기 위해 도형들은 Shape 클래스를 상속받아서 각자의 면적을 계산하는 getArea() 메서드를 구현하도록 하고, AreaCalculator 클래스는 Shape 인터페이스를 사용하여 다형성을 활용하여 계산하도록 수정하였습니다.
  * 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)
  서브 타입은 언제나 기반 타입으로 교체할 수 있어야 합니다. 즉, 상속 관계에 있는 클래스 간에는 기반 클래스의 인스턴스를 서브 클래스의 인스턴스로 대체할 수 있어야 합니다. 자식 클래스가 부모 클래스 역할을 할 수 있어야 함.
  
  ```
  class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  setWidth(width) {
    this.width = width;
  }

  setHeight(height) {
    this.height = height;
  }

  getWidth() {
    return this.width;
  }

  getHeight() {
    return this.height;
  }

  area() {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  setWidth(width) {
    this.width = width;
    this.height = width;
  }

  setHeight(height) {
    this.width = height;
    this.height = height;
  }
}

function increaseRectangleWidth(rectangle) {
  rectangle.setWidth(rectangle.getWidth() + 1);
}

const rectangle = new Rectangle(10, 20);
console.log(rectangle.area()); // 200
increaseRectangleWidth(rectangle);
console.log(rectangle.area()); // 220

const square = new Square(10, 10);
console.log(square.area()); // 100
increaseRectangleWidth(square); // LSP 위반!
console.log(square.area()); // 121 (예상치 못한 값 출력) ```
    

*  위의 코드에서 Square 클래스는 Rectangle 클래스를 상속 받았습니다. 하지만 Square 클래스에서 setWidth()와 setHeight() 메서드를 오버라이딩하면서 width와 height를 항상 같게 설정하도록 구현했습니다. 이러한 구현 방식은 Square가 Rectangle의 자식 클래스인 것이지만 Rectangle과 동작이 다르기 때문에 LSP를 위반하게 됩니다.


  ```
  //good
  javascript
  class Shape {
    area() {
      throw new Error("Area method should be implemented");
    }
  }

    class Rectangle extends Shape {
      constructor(width, height) {
        super();
        this.width = width;
        this.height = height;
      }

      setWidth(width) {
        this.width = width;
      }

      setHeight(height) {
        this.height = height;
      }

      getWidth() {
        return this.width;
      }

      getHeight() {
        return this.height;
      }

      area() {
        return this.width * this.height;
      }
      }

      class Square extends Shape {
        constructor(length) {
          super();
          this.length = length;
        }

        setLength(length) {
          this.length = length;
        }

        getLength() {
          return this.length;
        }

        area() {
          return this.length * this.length;
        }
      }

      function increaseShapeArea(shape) {
        // shape.area()가 제대로 구현되어 있다는 가정 하에
        const currentArea = shape.area();
        const newArea = currentArea + 1;
        return newArea;
      }

      const rectangle = new Rectangle(10, 20);
      console.log(rectangle.area()); // 200
      console.log(increaseShapeArea(rectangle)); // 201

      const square = new Square(10);
      console.log(square.area()); // 100
      console.log(increaseShapeArea(square)); // 101 
      ```

  * 인터페이스 분리 원칙 (Interface Segregation Principle, ISP)
  클라이언트는 자신이 사용하지 않는 인터페이스에 의존하지 않아야 합니다. 즉, 인터페이스를 세분화하여 클라이언트가 필요로 하는 기능만 제공하도록 해야 합니다.
  
    ```
    // bad
    interface SmartPrinter {
    print();
    fax();
    scan();
    }

    class AllInOnePrinter implements SmartPrinter {
      print() {
        // ...
      }  
      
      fax() {
        // ...
      }

      scan() {
        // ...
      }
    }

  class EconomicPrinter implements SmartPrinter {
    print() {
      // ...
    }  
    
    fax() {
      throw new Error('Fax not supported.');
    }

    scan() {
      throw new Error('Scan not supported.');
    }
  }
    ```
    ```
    //good
    interface Printer {
    print();
    }

    interface Fax {
      fax();
    }

    interface Scanner {
      scan();
    }

    class AllInOnePrinter implements Printer, Fax, Scanner {
    print() {
      // ...
    }  
    
    fax() {
      // ...
    }

    scan() {
      // ...
    }
  }

  class EconomicPrinter implements Printer {
    print() {
      // ...
    }
  }
  ```
  * 의존 역전 원칙 (Dependency Inversion Principle, DIP)
  추상화된 것은 구체적인 것에 의존하면 안 됩니다. 즉, 고수준 모듈은 저수준 모듈에 의존해서는 안 되며, 추상화된 인터페이스나 추상 클래스에 의존해야 합니다.
  ```
  //good
  class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, ${this.name}!`);
  }
}

class UserManager {
  constructor() {
    this.users = [];
  }

  addUser(user) {
    this.users.push(user);
  }

  greetAllUsers() {
    for (let user of this.users) {
      user.greet();
    }
  }
}

const user1 = new User('John');
const user2 = new User('Jane');
const userManager = new UserManager();
userManager.addUser(user1);
userManager.addUser(user2);
userManager.greetAllUsers();
```
위 코드에서 UserManager 클래스는 User 클래스에 의존하고 있습니다. UserManager 클래스는 User 클래스의 인스턴스를 생성하여 사용하고 있으며, 이를 통해 UserManager 클래스와 User 클래스는 긴밀한 결합을 가지게 됩니다. 이로 인해 User 클래스가 수정되면 UserManager 클래스도 수정해야 하므로 유지보수가 어려워집니다.

다음은 DIP를 적용한 코드 예시입니다.
  ```
  //good
  javascript

  class User {
    constructor(name) {
      this.name = name;
    }

    greet() {
      console.log(`Hello, ${this.name}!`);
    }
  }

  class UserManager {
    constructor(userRepository) {
      this.userRepository = userRepository;
    }

    addUser(user) {
      this.userRepository.save(user);
    }

    greetAllUsers() {
      const users = this.userRepository.getAllUsers();
      for (let user of users) {
        user.greet();
      }
    }
  }

  class UserRepository {
    constructor() {
      this.users = [];
    }

    save(user) {
      this.users.push(user);
    }

    getAllUsers() {
      return this.users;
    }
  }

  const user1 = new User('John');
  const user2 = new User('Jane');
  const userRepository = new UserRepository();
  const userManager = new UserManager(userRepository);
  userManager.addUser(user1);
  userManager.addUser(user2);
  userManager.greetAllUsers();
  ```

* 로컬 스토리지란 무엇인가요? 로컬 스토리지의 내용을 개발자 도구를 이용해 확인하려면 어떻게 해야 할까요?
  * 로컬 스토리지는 브라우저에서 제공하는 웹 스토리지 기술 중 하나로, 웹 애플리케이션이 사용자 브라우저 내부에 데이터를 저장하고 관리할 수 있도록 해줍니다. 이를 통해 사용자가 애플리케이션을 이용하는 동안에도 데이터를 유지하거나, 필요한 경우 데이터를 로드하여 더 나은 사용자 경험을 제공할 수 있습니다.

  로컬 스토리지의 내용을 개발자 도구를 이용해 확인하려면, 브라우저의 개발자 도구를 열고 Application 탭으로 이동합니다. 그리고 좌측 메뉴에서 "Storage" 섹션을 선택하면 로컬 스토리지를 확인할 수 있습니다. 이 섹션에서 "Local Storage"를 선택하면 로컬 스토리지에 저장된 키-값 쌍을 확인할 수 있으며, "Session Storage"를 선택하면 세션 스토리지에 저장된 키-값 쌍을 확인할 수 있습니다. 또한, 이 탭에서 스토리지를 수정하거나 삭제하는 것도 가능합니다.

  예를 들어 Chrome 브라우저에서는 개발자 도구를 열고 "Application" 탭을 클릭합니다. 그런 다음 "Storage" 섹션에서 "Local Storage" 또는 "Session Storage"를 선택합니다. 이를 통해 해당 스토리지에 저장된 데이터를 확인하고, 필요한 경우 수정하거나 삭제할 수 있습니다.

## Quest
* 외부 라이브러리나 프레임워크를 사용하지 않고, 자바스크립트를 이용하여 간단한 웹브라우저 기반의 텍스트 에디터를 만들어 보겠습니다.
  * 기본적으로 VSCode와 같이 탭을 이용해 여러 개의 파일을 동시에 편집할 수 있습니다.
  * 탭을 눌러 열려 있는 다른 파일을 편집할 수 있으며 탭을 언제든지 닫을 수 있습니다.
  * VSCode와 같이 새 파일, 로드, 저장, 다른 이름으로 저장 등의 기능을 가집니다. 저장은 웹 브라우저의 로컬 스토리지를 이용합니다.
  * VSCode와 같이 탭이 수정되었는데 저장되기 이전일 경우 이를 알려주는 인디케이터가 작동합니다.
  * 같은 이름의 파일을 저장할 경우 에러를 표시해야 합니다.
* 이번 퀘스트의 결과물은 앞으로의 많은 퀘스트에서 재사용되게 되니, 주의깊게 코드를 작성해 보세요!

## Advanced
* 웹 프론트엔드 개발에서 이러한 방식의 패턴을 더 일반화해서 정리할 수 있을까요? 이 퀘스트에서 각각의 클래스들이 공통적으로 수행하게 되는 일들에는 무엇이 있을까요?
