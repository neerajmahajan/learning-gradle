# learning-gradle
* checking the version
  * gradle -v
##### Groovy Basics
* String can be put in either '' or "" "", String puts in '' are java string whereas string puts in "" "" are groovy strings. string interpolation will not work in java string. see eg belows
    * Below code snippet will print Hello Neeraj
    ```
     String name = 'Neeraj'
     def name2 = 'Ram'  // We can either use specific data type or simply def
     println "Hello ${name}"
     println "Hello $name2" // We can either use ${variableName} or simply $variableName
    ```
    * Below code snippet will print Hello ${name}
    ```
     String name = 'Neeraj'
     println 'Hello ${name}'     
    ```
* Less import statments required. because it automatically inlucdes lot of java. packages by default.
* @ToString(includeNames=true) 
 * Generates toString method implementation
* @EqualsAndHashCode
 * Generated equals and hash code method implementaion taking the instance variables
* @TupleConstructor
 * Generates constructor method implementation taking all instance variables.
* @Canonical includes @ToString, @EqualsAndHashCode, @TupleConstructor
    
###### POGO similar to POJO in java, but with extra features
  * by default instance variables are private by default.
  * by default methods are public by default.
  * We don't need to provide setter method in a class. They are automatically available.
   * However if we specify either private or public with variables, then setter or getters method will not be auto generated.
  * We don't need to put **return** keyword at the end of method. It will automatically return;
  
  ```
  class Person {
   String first
   String last
  } 
     Person p = new Person()
  Or Person p = new Person(first: 'Neeraj' , last: 'Mahajan') // This statement will use the default constructor and will call the getters.
  
     p.setFirst('Neeraj') // setter method is provided internally by groovy.
     p.last = 'Mahajan'   // last variable is private so not accessible. but internally groovy is calling a setter method.
     println "${p.getFirst()} ${p.last}" // again p.last is actually calling getter method. 
  
  ```
  
  * If we use below @ToString annotation, it will automatically provide toString method implementation
  ```
  import groovy.transform.*
  @ToString(includeNames=true) // Abstract Syntaxt tree transformation 
  // Or @ToString() // This will not include properties name in the output
  class Person {
   String first
   String last
  } 
    
  Person p = new Person(first: 'Neeraj' , last: 'Mahajan')
  println p
  
  ```
  * Set Example
  ```
  import groovy.transform.*
  @Canonical  
  class Person {
   String first
   String last
  } 
    
  Person p = new Person(first: 'Neeraj' , last: 'Mahajan')
  Person p1 = new Person('Neeraj','Mahajan')
  println p
  println p1
  println p == p1
  
  Set persons = [p,p1]
  println persons.size()
  
  ```
  
  
