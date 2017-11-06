---
layout: post
title: "Kotlin vs Java"
---

Naujos JVM (Java Virtual Machine) programavimo kalbos Kotlin apžvalga ir palyginimas su Java.

## Kotlin vs Java
**Turinys**
- [Kotlin programavimo kalba](#kotlin-programavimo-kalba)
- [Overloaded methods](#overloaded-methods) 
- [FIlter usage collections](#filter-usage-collections) 
## Kotlin vaizdinė medžiaga internete
- [https://www.youtube.com/watch?v=H_oGi8uuDpA&t=2s]
- [https://www.youtube.com/watch?v=sZWMPYIkNd8&t=3417]
https://www.youtube.com/watch?v=pjC8C1xid3k
Kotlin in Android [https://www.youtube.com/watch?v=fPzxfeDJDzY&t=4s]
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
### Kotlin Pairs ir Triples

```kotlin 
fun grazinaPora(): Pair<String, String>{
    return Pair("Kaire", "Desine")
}
fun init(){
    val pora = grazinaPora()
    println("Pirmas narys: ${pora.first}, Antras narys: ${pora.second}")
}
```
Išvedamas tekstas į ekraną:
``` Pirmas narys: Kaire, Antras narys: Desine.```
Aiškumui įvesti galima pakeisti first, second,..., ir t.t. į savo sugalvotus pavadinimus pvz:
```kotlin
fun init(){
    val pora = grazinaPora()
    val (kaire_ranka, desine_ranka) = grazinaPora()
    println("Pirmas narys: "+ kaire_ranka + ", Antras narys:" + desine_ranka)
    println("Pirmas narys: ${pora.first}, Antras narys: ${pora.second}")
}
```
Jeigu reikšmė yra nesvarbi naudojant reikšmių pervadinimą (angl. destructuring declarations) galima pavadinti naudojant underscore:
```kotlin
 val (_, kita_reiksme) = grazinaPora()
 ```
### TypeAlias Kotlin 
Jeigu naudosime šį typealias mes pakeičiame String į Int, gali būti situacija, kai reikia modifikuoti atgyvenusį kodą (angl. deprecated), kadangi pakeitus visur kompiliatorius pažymės raudonai tada galie nesunkiai pašalinti šį kodą arba pakeisti. 
```kotlin 
typealias String = Int
```

### Conditions kotlin<TODO -------------> https://www.youtube.com/watch?v=YbF8Q8LxAJs
    


### Extension funkcijos 

Šios extension funkcijos yra labai patogios jeigu nusprendėte aprašyti naują funkciją jau egzistuojančioje klasėje.
Nereikia papildomai sukurti klasės tada paveldėti ją ir galiausiai papildyti nauju metodu. Kotlin naudoja šią paprastą konstrukciją:
```kotlin
// Duomenų klasė Studentas 
data class Studentas(val vardas: String, var amzius: Int)

// Esamom klasėm "Bet kuriai egzistuojančiai" galima papildyti naujomis funkcijomis pvz: 
fun Studentas.suteiktiStipendija(){
    println("Studentui suteikta stipendija")       
}

// Klasė Studentas papildyta nauja funkcija tikrinam naujai sukurtą metodą.
fun extensionFunkcijosTestas(){
    val stud = Studentas("Joniukas", 15)
    stud.suteiktiStipendija()
}
```
Į ekraną bus išvedamas šis tekstas: 
```Studentui suteikta stipendija```

Taip pat dar vienas pavyzdys turime String klasę, kuria papildysime nauju metodu pvz: 
```kotlin
fun String.pasisveikinimas(){
    println("Sveiki aš esu simbolių eilutė: (angl. String)")
}
fun extensionStringTestas(){
    val testas = String()
    testas.pasisveikinimas()
    "bet_kokia_simboliu_eilute".pasisveikinimas()
}
```
Į ekraną bus išvedamas šis tekstas:
``` Sveiki aš esu simbolių eilutė: (angl. String)
Sveiki aš esu simbolių eilutė: (angl. String)
```

Funkcija skaičiuojanti faktorialą naudojant rekursiją.


### Operatorių perkrovimas

Operatorių pekrovimas yra tik Kotlin kalboje panašumai lyginant su C++ kalba, kurioje taip pat yra galimybė naudoti perkrautuosius operatorius. Žemiau yra pateikiamas pavyzdys kaip galima panaudoti (plus (+)) operatorių norint susumuoti keletą skirtingų objektų pagal svorį:

```kotlin
package overloadedoperators

enum class MatavimoVnt(val svoris: Int){
    KILOGRAMAS (1000),
    GRAMAS (1),
    TONA (1_000_000)
}
interface VaisiausSvoris{
     fun svoris(): Int
}
class Pintine {
    private val sarasas : MutableList<Vaisius> = mutableListOf()
    fun idetiIpintine(vaisius: Vaisius) = sarasas.add(vaisius)
    fun pasverti(matas: MatavimoVnt = MatavimoVnt.GRAMAS):Int {
       return sarasas.sumBy { it -> it.svoris } / matas.svoris
    }
}

// Perkrauto operatoriaus (angl. overloaded operator) aprašymas 
open class Vaisius(val pavadinimas: String, var svoris: Int){
    operator fun plus(vaisius: Vaisius) : Vaisius{
        return Vaisius(pavadinimas, svoris + vaisius.svoris)
    }
}

class Slyva(pavadinimas:String, svoris: Int):
        Vaisius(pavadinimas, svoris), VaisiausSvoris{
    override fun svoris(): Int = svoris
}
class Kriause(pavadinimas:String, svoris: Int):
        Vaisius(pavadinimas, svoris), VaisiausSvoris{
    override fun svoris(): Int = svoris
}
class Obuolys(pavadinimas: String, svoris: Int):
        Vaisius(pavadinimas, svoris), VaisiausSvoris{
    override fun svoris(): Int = svoris
}

fun main(args: Array<String>) {
    val slyva = Slyva("Anašpet", 100)
    val obuolys = Obuolys("Auksis", 300)
    val kriause = Kriause("Aluona ", 350)
    var rezultatas = slyva + obuolys + kriause

    val pintine = Pintine()
    for (i in 1..20000) {
        pintine.idetiIpintine(slyva)
        pintine.idetiIpintine(obuolys)
        pintine.idetiIpintine(kriause)
    }
    println("Viso vaisių idėtų į pintinę: ${pintine.pasverti()} g")
    println("Viso vaisių idėtų į pintinę: ${pintine.pasverti(MatavimoVnt.KILOGRAMAS)} kg")
    println("Viso vaisių idėtų į pintinę: ${pintine.pasverti(MatavimoVnt.TONA)} t")
    println("Viso vaisių naudojant overloaded operatorių (plus (+)): ${rezultatas.svoris} g")
}
```
Įvykdžius programą į ekraną išvestas tekstas:
```
Viso vaisių idėtų į pintinę: 15000000 g
Viso vaisių idėtų į pintinę: 15000 kg
Viso vaisių idėtų į pintinę: 15 t
Viso vaisių naudojant overloaded operatorių (plus (+)): 750 g
```


https://www.programiz.com/kotlin-programming/operator-overloading






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
### Singleton Design pattern 
Klasikinis projektavimo šablonas Singleton naudojant java programavimo kalbą.
```java
package singletonai;

public class Singleton {
    private static Singleton instance = null;
    protected Singleton() {
        // Exists only to defeat instantiation.
    }
    public static Singleton getInstance() {
        if(instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
//--------------------------------------------Java-----------------------------------------------//
```

To pačio projektavimo šablono aprašymas naudojant programavimo kalbą kotlin.
```kotlin
package singletonai
object SingletonObject{
    val property = "kazkas"
}
//--------------------------------------------Kotlin-----------------------------------------------//
```


[Link to another page: HomePage]({{ site.baseurl }}/index).


