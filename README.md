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

2. In addition to reusing the immutable objects, we can also reuse the mutable objects if we know that they won't be modified.
    Ex: Date object.
        
3. Keep an eye on the expensive objects in the program.

4. Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.

5. Creating additional objects to enhance the clarity, simplicity, or power of a program is generally a good thing.

6. Avoiding object creation by maintaining our own object pool is bad idea unless the objects in the pool are extremely heavyweight.
   Ex: database connection

**Eliminate obsolete object references**

1. *What is obsolete reference?*
A. An obsolte reference is simply a reference that will never be dereferenced again.

2. *What is the problem with obsolete reference?*
A. An obsolte reference causes memory leak. It can cause disk paging and even program failure with in OutOfMemeoryError.

3. *How to avoid obsolte references?*
A. Nullinig out object references will make them available to garbage collector. But if they are subsequently referenced by the other
   objects in the program the program will fail with a NullPointerException. The best way to eliminate an obsolete references is to let    the variable that contained the reference fall out of scope. This occurs naturally if we define each variable in the narrowest 
   possible scope.
   
> Another common source of memory leaks is cache. Once we put an object reference into cache, we may forget that it's there and leave it
  in the cache long after it become irrelevant.
 
4. *How can we avoid memory leaks through cache?*
A.  One solution is to represent the cache as a **WeakHashMap** , where the entries will be removed automatically after they become 
    Obsolete. But remember that WeakHashMap is useful only if the desired lifetime of cache entries is determined by external references
    to the key, not the value.
    
    **LinkedHashMap** provides the facility to remove the entries that have fallen into disuse with its **removeEldestEntry** method.
    
    Take a look at *java.lang.ref* for more sophisticated caches.

> A third common source of memory leaks is listeners and other callbacks.

  *If we implement an API where clients register callbacks but don't deregister them explicitly, they will accumulate unless you take
  some action. The best way to ensure that callbacks are garbage collected promptly is to store only weak references to them, for 
  instance, by storing them only as keys in a **WeakHashMap** . *
  
  > Memory leaks can be discovered by the careful inspection of the code or by using the debuggint tools like **heap profiler** .
  
  
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
