---
layout: post
title: "KOTLIN VS JAVA"
---

Naujos JVM (Java Virtual Machine) programavimo kalbos Kotlin apžvalga ir palyginimas su Java.

## KOTLIN VS JAVA


**Java methods overloading**
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
```

**Kotlin methods overloading**

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
}
```

[Link to another page: HomePage]({{ site.baseurl }}/index).


