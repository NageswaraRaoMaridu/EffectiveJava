## Learning Java in-depth:
Exploring the concepts of java in-depth.

**what is telescoping constructor?**






**Enforcing noninstantiability with a private constructor:**

1. A class can be made noninstantiable by including a private constructor. So the class will never be instantiated under any circumstances.
   But the side effect of this idiom is, it also prevents the class from being subclassed. All the constructors must invoke a super class
   constructor explicitly or implicitly. And a subclass constructor would have no accessible superclass constructor to invoke.
   
2. why exactly do subclass constructors have to explicitly call super class constructor?

   Java requires that every class to be initialized by some constructor.If there isn't a default constructor, the java compiler has no way of knowing which constructor to 
   call, or what parameters need to be passed. If there isn't a default constructor on a class, one of its other constructors must be called for the object to be 
   initialized.
   
3. why does java calls the super class default constructor even when we declare only a parameterized constructor(no default constructor)?
   
   Java gaurantees that the constructor method of a class is called whenever an instance of that class is created. It also gaurantees that the constructor is called
   whenever an instance of any subclass is created. Thus if the first statement in a constructor doesn't explicitly invoke another constructor with this() or super(), java
   implicitly inserts the call super(); nothing but the superclass constructor with no arguments. This also explain us that the constructor calls are chained.
   
   when a constructor is invoked, it can count on the fields of it's superclass to be initialized.
   
4. what if the super class don't have a default constructor?

   If a class does not define a no-argument constructor, all its subclasses must define constructors that explicitly invoke the super class constructor with necessary
   arguments.
   
5. what is shadowed field?

   Sometimes the subclasses contains the same fields as their super classes. In that case, we say that fields of sub class shadows the field of super class. we can access
   the fields of the super class using the super keyword.
   
   If class C extends B and B extends A. All the classes have a field called X.
   
   From the class C how can we access the field(X) of other classes.
   ```
   X            ----------> X in C
   super.X      ----------> X in B
   ((B) this).X ----------> X in B
   ((A) this).X ----------> X in A
   
   super.super.x   ------> Illegal
   ```


**Avoid creating unnecessary objects:**

1. An object can always be re-used if it is immutable.

2. 
