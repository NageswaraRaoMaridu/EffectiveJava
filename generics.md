
1. What is the purpose of generic type arguments in the generic method?  
Generic methods allow type parameters to be used to express dependencies among the one or more arguments to a method and/or it's return type.If there is not such dependency, generic method should not be used
  
2. What is raw type?  
When a generic type like Collection is used without type parameter, it's called a raw type.
  
Note: Generics are implemented by the Java compiler as a front-end conversion called 'erasure'. We can think of this as a source-to-source translation. Erasure gets rid of(or erases) the generic type information. All the type information between the angle brackets is thrown out.
