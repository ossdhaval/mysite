# Java annotations and Custom annotations

### Reference:
- Could not find updated tutorial for OpenJDK 17 about annotations. Java tutorials for most subjects are still pointing to JDK 8. So, link below may be old but basics would be the same.

https://docs.oracle.com/javase/tutorial/java/annotations/index.html

### What is annotation and what are different usecases:

Annotations, a form of metadata, provide data about a program that is not part of the program itself. Annotations have no direct effect on the operation of the code they annotate.

Annotations have a number of uses, among them:

- Information for the compiler — Annotations can be used by the compiler to detect errors or suppress warnings.
- Compile-time and deployment-time processing — Software tools can process annotation information to generate code, XML files, and so forth.
- Runtime processing — Some annotations are available to be examined at runtime.

### where can it be used:

### About parameters to annotations

```
The annotation can include elements, which can be named or unnamed, and there are values for those elements:

@Author(
   name = "Benjamin Franklin",
   date = "3/27/2003"
)
class MyClass { ... }
or

@SuppressWarnings(value = "unchecked")
void myMethod() { ... }
If there is just one element named value, then the name can be omitted, as in:

@SuppressWarnings("unchecked")
void myMethod() { ... }
If the annotation has no elements, then the parentheses can be omitted, as shown in the previous @Override example.

It is also possible to use multiple annotations on the same declaration:

@Author(name = "Jane Doe")
@EBook
class MyClass { ... }
```

### defining custom annotations:

Many annotations replace comments in code.

Suppose that a software group traditionally starts the body of every class with comments providing important information:

```
public class Generation3List extends Generation2List {

   // Author: John Doe
   // Date: 3/17/2002
   // Current revision: 6
   // Last modified: 4/12/2004
   // By: Jane Doe
   // Reviewers: Alice, Bill, Cindy

   // class code goes here

}
```

To add this same metadata with an annotation, you must first define the annotation type. The syntax for doing this is:

```
@interface ClassPreamble {
   String author();
   String date();
   int currentRevision() default 1;
   String lastModified() default "N/A";
   String lastModifiedBy() default "N/A";
   // Note use of array
   String[] reviewers();
}
```

The annotation type definition looks similar to an interface definition where the keyword interface is preceded by the at sign (@) (@ = AT, as in annotation type). Annotation types are a form of interface.

After the annotation type is defined, you can use annotations of that type, with the values filled in, like this:

```
@ClassPreamble (
   author = "John Doe",
   date = "3/17/2002",
   currentRevision = 6,
   lastModified = "4/12/2004",
   lastModifiedBy = "Jane Doe",
   // Note array notation
   reviewers = {"Alice", "Bob", "Cindy"}
)
public class Generation3List extends Generation2List {

// class code goes here

}
```

### predefined annotations:

- @Deprecated
- @Override
- @SuppressWarnings
- @SafeVarargs
- @FunctionalInterface
meta-annotations (annotations that apply to other annotations)
- @Retention
    ```
    RetentionPolicy.SOURCE – The marked annotation is retained only in the source level and is ignored by the compiler.
    RetentionPolicy.CLASS – The marked annotation is retained by the compiler at compile time, but is ignored by the Java Virtual Machine (JVM).
    RetentionPolicy.RUNTIME – The marked annotation is retained by the JVM so it can be used by the runtime environment.
    ```
- @Documented
    - annotation indicates that whenever the specified annotation is used those elements should be documented using the Javadoc tool. (By default, annotations are not included in Javadoc.) 
    
- @Target
  - annotation marks another annotation to restrict what kind of Java elements the annotation can be applied to.
    - ElementType.ANNOTATION_TYPE can be applied to an annotation type.
    - ElementType.CONSTRUCTOR can be applied to a constructor.
    - ElementType.FIELD can be applied to a field or property.
    - ElementType.LOCAL_VARIABLE can be applied to a local variable.
    - ElementType.METHOD can be applied to a method-level annotation.
    - ElementType.PACKAGE can be applied to a package declaration.
    - ElementType.PARAMETER can be applied to the parameters of a method.
    - ElementType.TYPE can be applied to any element of a class.
    
 - @Inherited
  - annotation indicates that the annotation type can be inherited from the super class. (This is not true by default.) When the user queries the annotation type and the class has no annotation for this type, the class' superclass is queried for the annotation type. This annotation applies only to class declarations.
  
- @Repeatable
  - indicates that the marked annotation can be applied more than once to the same declaration or type use
  
  
### Type Annotations and Pluggable Type Systems

Before the Java SE 8 release, annotations could only be applied to declarations. As of the Java SE 8 release, 
annotations can also be applied to any type use. This means that annotations can be used anywhere you use a type. 
A few examples of where types are used are class instance creation expressions (new), casts, implements clauses, 
and throws clauses. This form of annotation is called a type annotation.
