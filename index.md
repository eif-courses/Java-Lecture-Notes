---
#
# Here you can change the text shown in the Home page before the Latest Posts section.
#
# Edit cayman-blog's home layout in _layouts instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: home
---


# JAVA
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
# KOTLIN
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
