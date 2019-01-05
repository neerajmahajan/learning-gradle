# learning-gradle
* checking the version
  * gradle -v
###### Groovy Basics
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
    
  ###### POGO similar to POJO in java, but with extra features
  * by default instance variables are private by default.
  * by default methods are public by default.
  * We don't need to provide setter method in a class. They are automatically available.
  
  ```
  class Person {
   String first
   String last
  } 
  Person p = new Person()
  p.setFirst('Neeraj') // setter method is provided internally bu groovy.
  p.last = 'Mahajan'   // last variable is private so not accessible. but internally groovy is calling a setter method.
  println "${p.getFirst()} ${p.last}" // again p.last is actually calling getter method. 
  
  ```
