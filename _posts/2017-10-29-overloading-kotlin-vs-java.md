---
layout: post
title: "Kotlin vs Java"
---

Naujos JVM (Java Virtual Machine) programavimo kalbos Kotlin apžvalga ir palyginimas su Java.

## Kotlin vs Java
**Turinys**
- [Kotlin programavimo kalba] (#kotlin-programavimo-kalba)
- [Overloaded methods](#overloaded-methods) 
- [FIlter usage collections](#filter-usage-collections) 



### Kotlin programavimo kalba

**Kotlin funkcija**
Kotlin nesudėtingos funkcijos aprašomos vienu sakiniu nereikia "{....}" pvz:  
```kotlin  
fun sudeti(a: Int, b: Int) = a + b
```
Kotlin funkcija, kuri nieko negrąžina aprašoma taip: 
```kotlin 
    fun zinute(tekstas: String): Unit{ // Pagal nutylėjimą grąžina Unit tipą (Unit neprivaloma rašyti).
        println("Sveikas: $tekstas")
}
```
**Kotlin kintamieji**
Kotlin turi tik šiuos kintamųjų aprašymo būdus **val** arba **var** žemiau pateikiami skirtumai: 
```kotlin

val skaicius = 50 // reikšmė, kurios negalime keisti (angl. immutable)
var vardas = "Petras" // Vardą galėsime pakeisti bet kada (angl. mutable)

```
**Kotlin data class**
Kotlin turi galimybę įgyvendinti duomenų klases vadinamas data class žemiau matysite kaip nesudėtingai galima aprašyti senąsias JAVA bean klases (POJO / POCO):
```kotlin 
data class Studentas(val vardas: String, var amzius: Int)
```
**Pastaba**. data class negali būti paskelbtos abstrakčiomis klasėmės, taip pat negali būti galutinės (angl. sealed) arba vidinės (angl. inner). Sukūrus data class yra sugeneruojami šie metodai: get/set, toString, hashCode, copy metodai. Norint nukopijuoti reikšmę iš sukurto objekto egzemplioriaus pvz: 
```kotlin 
val petriukas = Studentas("Petriukas", 22)
    val kitasPetriukas = petriukas.copy(amzius = 25)
    println(kitasPetriukas) // Studentas(vardas=Petriukas, amzius=25)

``` 

**Data Classes and Destructuring Declarations**

Component functions generated for data classes enable their use in destructuring declarations:
```kotlin
val jane = User("Jane", 35) 
val (name, age) = jane
println("$name, $age years of age") // prints "Jane, 35 years of age"
```
**Standard Data Classes**

The standard library provides Pair and Triple. In most cases, though, named data classes are a better design choice, because they make the code more readable by providing meaningful names for properties.

### Overloaded methods


Overloaded metodai Java kalboje aprašomi kiekvienam atvejui turi skirtis parametrų skaičius arba perduodamas tipas pvz: turime tokią aibę metodų: 
```Java 
  void metodas(){}
  void metodas(int a){}
  void metodas(double c){}
  void metodas(int a, double c){}
  void metodas(double c, int a){}
```
Kotlin kalboje šiek tiek paprasčiau kadangi yra įvedami įvardintieji parametrai (angl. named parameters) ir funkcijų parametrai gali turėti reikšmę pagal nutylėjimą (angl. by default) kas įgalina paprastesnį ir lankstesnį overloaded metodų aprašymą. Apžvelkime prieš tai aprašytą Java metodą realizuojant analogiškus metodus naudojant Kotlin programavimo kalbą. Kadangi Kotlin neturi metodų turi funkcijas tada galima aprašyti funkciją atitinkančią prieš tai aprašytuosius metodus Java kalboje. 

```kotlin
fun metodas(a: Int = 0, c: Double = 0.0) { // Žymiai paprasčiau nereikia aprašyti visų įmanomų atvejų!!!
    metodas()
    metodas(10)
    metodas(c = 33.9)
    metodas(55, 22.9)
    metodas(c = 22.8, a = 2)
}

```
**Dar vienas pavyzdys palyginimui Java vs Kotlin aprašant overloaded metodus**

```java
package overloadedMethods;

public class OverloadedMethodJava {
    void printMessage(String message){ 
      System.out.printf("Message: %s\n", message); 
    }
    void printMessage(String message, String prefix){ 
      System.out.printf("Message: %s, Prefix: %s\n", message, prefix); 
    }
    void printMessage(String message, String prefix, String suffix){ 
      System.out.printf("Message: %s, Prefix: %s, Suffix: %s\n", message, prefix, suffix); 
    }

    public static void main(String[] args) {
        new OverloadedMethodJava().printMessage("Hello");
        new OverloadedMethodJava().printMessage("Hello", "WithPRefix");
        new OverloadedMethodJava().printMessage("Hello", "WithPRefix", "AndSuffix");
    }
}
//--------------------------------------------Java-----------------------------------------------//
```

```kotlin
package overloadedMethods

class OverloadedMethodKotlin {
    fun printMessage(message: String, prefix: String = "", suffix: String = "") {
        println("$message $prefix $suffix")
    }
}
fun main(args: Array<String>) {
    val overloaded = OverloadedMethodKotlin() // Immutable readonly
    overloaded.printMessage("Hi im Kotlin")
    overloaded.printMessage("Hi im Kotlin", "with prefix")
    overloaded.printMessage("Hi im Kotlin", "with prefix", "AndSuffix")
    // Bet kokia tvarka pagal vardą parametro
    overloaded.printMessage(prefix = "Hello im Prefix", message = "im Kotlin", suffix = "And Suffix")

//--------------------------------------------Kotlin-----------------------------------------------//
```

### Filter usage collections


```java
public class ListExamples {
    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>(List.of(
                new Customer("Petras"),
                new Customer("Ona"),
                new Customer("Birute")
        ));
        customers.add(new Customer("Petras"));
        System.out.println("----------------------------");
        customers.forEach(System.out::print);
        IntStream intStream = IntStream.range(1, 100);
        intStream.filter(v -> v < 100)
                .mapToDouble(v -> v % 20)
                .forEach(System.out::print);
    }
}
//--------------------------------------------Java-----------------------------------------------//
```


```kotlin
package listOfNumbers
// In JAVA CUSTOMER CLASS AROUND 100 lines with basic methods:)
data class Customer(val name: String)
fun main(args: Array<String>) {
    val customers = ArrayList<Customer>(listOf<Customer>(
            Customer("Petras"),
            Customer("Jonas"),
            Customer("Jonas")
    ))
    customers.add(Customer("Ona"))
    println("--------------------------------")
    customers.forEach { print(" " + it.name) }

    // number 1 to 100 similar to IntStream in JAVA
    val numbers = 1..100
    numbers.filter { it < 100 }
            .map { it % 20 }
            .forEach { print(" " + it) }
}
//--------------------------------------------Kotlin-----------------------------------------------//
```






[Link to another page: HomePage]({{ site.baseurl }}/index).


