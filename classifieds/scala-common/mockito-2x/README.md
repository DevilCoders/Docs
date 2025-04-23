Adapted and extended version of https://github.com/j-griffith/mosckito

# mockito-2x

This is a wrapper for Mockito 2.x that is more safe and flexible for using in scala.

[Mockito](http://site.mockito.org/) is a mocking framework for writing unit tests. 

## Getting Mockito 

### Release Versions

The jars are hosted on [bintray](https://bintray.com/mockito) and are mirrored to Maven Central.
  
```
libraryDependencies += "org.mockito" % "mockito-core" % "2.2.22"
```

```
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>2.2.22</version>
    <scope>test</scope>
</dependency>

```


## MockitoSupport

This is a basic trait providing the most used Mockito functionality: creation of mocks and stubbing their method calls. There is also a same-named object allowing use imports instead of inheritance.

### Creating mocks

The trait provides overloaded methods called ```mock``` for mocks creation. The default version without parameters uses ```ThrowingAnswer``` as a default. Other versions allows to provide custom default answer or other Mockito settings.

Using of ```ThrowingAnswer``` makes mock to throw ```NotMockedException``` on each method call which was not stubbed explicitly. It allows to avoid undetermined behavior and unexpected exceptions (like NPEs) in tests and provides detailed information about problem method invocation. ```ThrowingAnswer``` ignores generated methods for [default arguments](http://docs.scala-lang.org/sips/completed/named-and-default-arguments.html), for them it uses ```Answers.RETURNS_DEFAULTS``` which returns type default. It is impossible to use standard Mockito mocking methods for mocks created with ```ThrowingAnswer```. 

It is necessary to remember that default arguments are compiled into methods which are mocked too, so calling method with defaults may get unexpected arguments. The best way is to pass desired values explicitly.
     
### Mocking in Mockito-style      
            
To mock invocation as in regular Mockito one can use method ```when```. It works as ```Mockito.when``` except that it allows to mock method which throws exception, so one have to use this method when create mock with ```ThrowingAnswer```.
               
This mocking style does not applicable for methods with Unit return type.                  
 
### Mocking with partial functions

The ```stub``` object provides mocking with partial functions. It works for methods with any return type and allow to use arguments for answer generating. As opposed to ```when``` each call of ```stub``` on the same method replaces previous stubbing. ```NotMockedException``` will be thrown if given partial function is not defined on some input.

## Restrictions

For now there is no way to mock method with call-by-name parameters.

## Examples

A lot of examples could be found in ```MockitoSupportSpec``` test. There is ```TestTrait``` in test companion object which contains different kinds of methods and is used for testing, it can help to find a solution for concrete situation.  