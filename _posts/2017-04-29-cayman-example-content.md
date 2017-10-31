---
layout: post
title: "Anotacijos ir JavaDocs"
---

# Anotacijos vs Komentarai

- One main difference with annotation is it can be carried over to runtime
and the other two stops with compilation level. Annotations are not only comments, it brings in new possibilities in terms of automated processing.
- Annotations, a form of metadata, provide data about a program that is not part of the program itself. Annotations have no direct effect on the
operation of the code they annotate.

# Anotacijų rūšys

**Class** - when the annotation value is given as ‘class’ then this annotation will be compiled and included in the class file.
**Runtime** - the value name itself says, when the retention value is ‘Runtime’ this annotation will be available in JVM at runtime. We can write custom code using reflection package and parse the annotation. I have give an example below.
 **Source** - his annotation will be removed at compile time and will not be available at
compiled class.

# Anotacijų paskirtis

- **Information for the compiler** — Annotations can be used by the compiler to detect errors or suppress warnings.
- **Compile-time and deployment-time processing** — Software tools can process annotation information to generate code, XML files, and so forth.
- **Runtime processing** — Some annotations are available to be examined at runtime.

# Kada nepatartina naudoti anotacijų

Do not over use annotation as it will pollute the code.
It is better not to try to change the behaviour of objects using
annotations. There is sufficient constructs available in oops and
annotation is not a better mechanism to deal with it.
We should not what we are parsing. Do not try to over generalize as it may complicate the underlying code. Code is the real program and annotation is meta.
Avoid using annotation to specify environment / application /
database related information.

**Anotacijos pavyzdys:**
```java
@Documented
@Target(ElementType.METHOD)
@Inherited
@Retention(RetentionPolicy.RUNTIME)
@interface ManoAnotacija{
   int studentAge() default 18;
   String studentName();
   String stuAddress();
   String stuStream() default "CSE";
}
```

