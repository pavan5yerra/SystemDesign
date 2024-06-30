

**Single Responsibility:**  A Class should have one responsibility to change



![image.png](https://eraser.imgix.net/workspaces/RHvayis7uYQNdrSqkxAk/2TpPe0m2nPZODyVZctbl8Rh7kLL2/a6RWV1d_8qrf1zLhfILUk.png?ixlib=js-3.7.0 "image.png")





```Javascript
  // Bad example
  class User {
    createUser(data) { /* ... */ }
    validateUser(data) { /* ... */ }
    sendEmail(user) { /* ... */ }
  }
  
  // Good example
  class User {
    createUser(data) { /* ... */ }
  }
  
  class UserValidator {
    validateUser(data) { /* ... */ }
  }
  
  class EmailService {
    sendEmail(user) { /* ... */ }
  }
```


** Open/Closed Principle (OCP) : ** Open for extenstion , closed for modification.



![image.png](https://eraser.imgix.net/workspaces/RHvayis7uYQNdrSqkxAk/2TpPe0m2nPZODyVZctbl8Rh7kLL2/ZKZvv03U6IrL7xXCehGAz.png?ixlib=js-3.7.0 "image.png")



```Javascript
// Bad example
class Rectangle {
  calculateArea() { /* ... */ }
}

class AreaCalculator {
  calculateShapeArea(shape) {
    if (shape instanceof Rectangle) {
      return shape.calculateArea();
    }
  }
}

// Good example
class Shape {
  calculateArea() { /* ... */ }
}

class Rectangle extends Shape {
  calculateArea() { /* ... */ }
}

class AreaCalculator {
  calculateShapeArea(shape) {
    return shape.calculateArea();
  }
}
```


Liskov Substitution Principle (LSP) : 

      The child class should perform all behaviors of the parent class,else there is some issue triggers in future.



![image.png](https://eraser.imgix.net/workspaces/RHvayis7uYQNdrSqkxAk/2TpPe0m2nPZODyVZctbl8Rh7kLL2/hkUiJp3ExvJSPoR2yxEUv.png?ixlib=js-3.7.0 "image.png")



```Javascript
// Bad example

class Person {
  see() { /* ... */}
}


class BlindSwordMan extends Person{
  cantSee(){/* */}  // violating principle
  sword() {}
}



//Good Example 

class Eye {
  see();
}

class Foot{
  walk();
}

class Hand{
   hold();
}


class CommonPerson extends Eye ,Foot , Hand {
  see();
  walk();
  hold();
}

class BlindPerson extends Foot , Hand {
  walk();
  hold();
}

class BlindSwordsMan extends BlindPerson {
    swordSkill();
}
```


**Interface Segregation:**

Many client-specific interfaces are better than one general purpose interface



![image.png](https://eraser.imgix.net/workspaces/RHvayis7uYQNdrSqkxAk/2TpPe0m2nPZODyVZctbl8Rh7kLL2/08kXzqFaDJLVgXp48QeBM.png?ixlib=js-3.7.0 "image.png")



```Javascript
//Bad Example

interface General {
  fly();
  run();
}

class Person extends General {
  run();
  fly(); // I can't fly - violates principle
}

class Wizard extends General {
  run();
  fly();
}

class SwordsMan extends General {
  run();
  fly(); // I can't fly - violates principle
}

// Good Example 
interface fly{
  fly();
}

interface run{
  run();
}

class Person extends  run{
  run();
}

class Wizard extends run , fly {
  run();
  fly();
}

```


**Dependency Inversion Principle (DIP):**

The design should depend on interfaces or abstract classes rather than concrete classes and functions. This promotes decoupling and flexibility.



![image.png](https://eraser.imgix.net/workspaces/RHvayis7uYQNdrSqkxAk/2TpPe0m2nPZODyVZctbl8Rh7kLL2/3WfwTN4djFEsgs0SbPED3.png?ixlib=js-3.7.0 "image.png")



![image.png](https://eraser.imgix.net/workspaces/RHvayis7uYQNdrSqkxAk/2TpPe0m2nPZODyVZctbl8Rh7kLL2/SHsqDyBduFG2hReaH2gy_.png?ixlib=js-3.7.0 "image.png")



