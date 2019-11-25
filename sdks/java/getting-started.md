# Getting started

## Hello world Java!

> We will use Unix-based commands. Windows has similar commands for each.

1. Create a new folder `JavaTest`  on your `$HOME` directory called.
2. Switch to `JavaTest` and create a subdirectory structure that will host our project: `src/main/java/hello` 

```bash
mkdir -p src/main/java/hello
```

1. Switch to `src/main/java/hello` and create the following `HelloWorld.java` file:

```java
package hello;

public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```

1. Go back to the root folder of your project `JavaTest` and initialice your project using `gradle`:

```bash
gradle init
```

You'll notice a few new files in your root folder. You can freely add them to your version control system so everyone can build it just the same way.

1. Edit the `build.gradle` file with your favourite editor and add:

```java
apply plugin: 'java'
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'
```

> Note that `mainClassName` must be fully qualified class name.

1. Let's build the source using the `gradlew` wrapper script that `Gradle` has just created:

```bash
./gradlew build

BUILD SUCCESSFUL in 2s
2 actionable tasks: 2 executed
```

The `build` argument is a task. Each project includes a collection of tasks, each of which performs a basic operation. `Gradle` comes with a set of predefined tasks that could be extended using an API. Managing tasks is out of the scope of this tutorial, but you can find more information about how to extend and configure tasks on [Gradle documentation](https://guides.gradle.org/).

A new folder `build/libs` has been created containing the `jar` file of your project.

1. And finally let's run it:

```bash
./gradlew run

> Task :run
Hello World

BUILD SUCCESSFUL in 0s
2 actionable tasks: 1 executed, 1 up-to-date
```

## Integrating Amadeus SDK

So far we have built a very simple piece of code. Let's do something cool by calling one of our [Flight Search APIs](https://developers.amadeus.com) from your Java code.

According to our [Java SDK](https://github.com/amadeus4dev/amadeus-java) documentation, we need to update our `build.gradle` file to include the following dependencies:

```java
compile 'com.google.code.gson:gson:2.8.5'
compile "com.amadeus:amadeus-java:1.1.2"
```

Our new `build.gradle` will look like:

```java
apply plugin: 'java'
apply plugin: 'application'

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile 'com.google.code.gson:gson:2.8.5'
    compile 'com.amadeus:amadeus-java:1.1.2'
}

repositories { maven { url "https://jcenter.bintray.com" } }

jar {
    baseName = 'amadeusExample'
    version =  '0.1.0'
}

mainClassName = 'AmadeusExample'
```

Note that we have added `repositories` in order to retrieve the `Amadeus Java SDK` jar file automtically during the `build` task.

It's time to call the APIs from our Java sample. Replace the previously created `HelloWorld.java` with the file `AmadeusExample.java`:

```java
import com.amadeus.Amadeus;
import com.amadeus.Params;

import com.amadeus.exceptions.ResponseException;

import com.amadeus.shopping.FlightDestinations;
import com.amadeus.resources.FlightDestination;

public class AmadeusExample {
  public static void main(String[] args) throws ResponseException {
    Amadeus amadeus = Amadeus
            .builder("YOU_CLIENT_ID","YOUR_CLIENT_SECRET")
            .build();

    FlightDestination[] flightDestinations = amadeus.shopping.flightDestinations.get(Params.with("origin", "MAD"));

    if (flightDestinations[0].getResponse().getStatusCode() != 200) {
        System.out.println("Wrong status code for Flight Inspiration Search: " + flightDestinations[0].getResponse().getStatusCode());
        System.exit(-1);
    }

    System.out.println(flightDestinations[0]);
  }
}
```

The sample calls [Flight Inspiration Search API](https://developers.amadeus.com/self-service/category/203/api-doc/3) in order to retrieve best offers departuring Madrid.

Finally, let's execute the sample:

```bash
./gradlew run

> Task :run
FlightDestination(type=flight-destination, origin=MAD, destination=BIO, departureDate=Sat Nov 17 00:00:00 CET 2018, returnDate=Wed Nov 21 00:00:00 CET 2018, price=FlightDestination.Price(total=92.26))
```

