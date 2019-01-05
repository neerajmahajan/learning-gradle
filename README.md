# learning-gradle
* checking the version
  * gradle -v
* String can be put in either '' or "" "", String puts in '' are java string whereas string puts in "" "" are groovy strings. string interpolation will not work in java string. see eg belows
   * Below code snippet will print Hello Neeraj
    ```
     String name = 'Neeraj'
     println "Hello ${name}"
    ```
    * Below code snippet will print Hello ${name}
    ```
     String name = 'Neeraj'
     println 'Hello ${name}'
    ```
