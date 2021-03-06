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
  ###### Collections
  
  * Array List
  
  ```
   def nums = [3,1,4,1,5,9]
   print nums  // output [3,1,4,1,5,9]
   print nums.class.name // Is actually nums.getClass().getName() // java.util.ArrayList
     
  ```
  
  * Linked List
  
  ```
   def nums = [3,1,4,1,5,9] as LinkedList
   print nums  // output [3,1,4,1,5,9]
   print nums.class.name // Is actually nums.getClass().getName() // java.util.LinkedList
     
  ```
  
  * Set
  
  ```
   def nums = [3,3,4,4,5,5] as Set
   print nums  // output [3,4,5]
   print nums.class.name // Is actually nums.getClass().getName() // java.util.LinkedHashSet
     
  ```
  
  * SortedSet
  
  ```
   def nums = [8,7,3,3,4,4,5,5] as SortedSet
   print nums  // output [3,4,5,7,8]
   print nums.class.name // Is actually nums.getClass().getName() // java.util.TreeSet
     
  ```
  
  * Iterating Collections
  
  ```
   def nums = [3,1,4,1,5,9]
   print nums  // output [3,1,4,1,5,9]
   
   for(int i=0;i++;i<nums.size) {println nums[i]};
   for(Integer i : nums) {println nums[i]}
   for(i in nums) {println nums[i]}
   nums.each {println it} // Using Closure // Be deault it is the default name // By defaul All closure has 1 argument ????
   nums.each {x -> println x}  // each method also returns the collection at end
   nums.eachWithIndex {n,index ->
    println "nums[$indez] $i"
   }
    
  ```
  
  * Doubling the value of collection
  
  ```
   // This approach is not recommended
    def nums = [1,2,3,4,5]
    def doublesNumber = []
    nums.each {doublesNumber << it * 2} // << appends to the collection. // we can modify the external varibale like doublesNumber
  ```
  * Recommneded approach
  ```
   // Recommneded approach
    def nums = [1,2,3,4,5]
    def doubleNumbers = nums.collect { it * 2} // collect is like a map in java // It applies the function on each collection variable and returns the new transformed collection.
  ```
  
  * Functions MFR - Map - Filter - Reduce example
  
  ```
   // Here collect is map, findAll is like filter and sum is like the reduce operation
    def nums = [1,2,3,4,5]
    println nums.collect { it * 2} .findAll {it % 2 == 0 } .sum()    
    
  ```
  * Map example
  ```
   def map = [a:1,b:2,c:3]
   println map               // [a:1,b:2,c:3]
   println map.keySet()      // [a,b,c]
   println map.values()      // [1,2,3]
   println map.entrySet()    // [a=1,b=2,c=3]
   
   map.d = 4                 // Add new Key value
   map['e'] = 5              // Add new Key value
   map.put('f',6)
   
   map.each {e ->  println "${e.key} === ${e.value}"}
   map.each {key,value -> println "$key === $value" }
   map.collect {key,value -> key * value} // print [a,bb,ccc]
  ```
  
  * REST API CALL example
  
  ```
  String base = 'https://maps.googleapis.com/maps/api/geocode/xml'
  def encoded = ['12 Hight Street', 'Southampton','UK']
       .collect {URLEncoder.encode(it, 'UTF-8')}
       .join(',')
       
  String qs = "address=$encoded"
  def xmlRoot = new XmlSlurper().parse("$base$qs")
  def loc = root.result[0].geometry.location
  println "(${loc.lat}, ${loc.lng})") 
  
  ```
  
  
  ##### Gradle build instructions
  * Gradle tasks are equal to Maven phases
  * **apply plugin: 'java'** // Here apply is method call from POGO class, plugin is a property in POGO and 'java' is the value for the argument.
  
  #### Creating a java based project structure from gradle tool
  
  * gradle init --type java-library // https://guides.gradle.org/building-java-applications/ gradle init --type java-application
  
  
  
  
  
  
