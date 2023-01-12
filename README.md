# Description of design patterns with js examples.

I might start a blog at some point, but this seemed the path of least resistance at this point. So, we'll start and build iteratively. Agile, you know!

## Singleton Design Pattern: When One is the Loneliest Number

When it comes to object-oriented programming, the singleton design pattern is like that one person at the party who always wants to dance alone. But just like that person, the singleton pattern can actually be pretty useful in certain situations.

So, what exactly is the singleton pattern? In a nutshell, it's a way to ensure that a class only has one instance, and that there's a global point of access to that instance.

Why would you want to do this? Well, let's say you're building a game and you only want one player character. Or maybe you're working on a financial application and you only want one database connection. These are both situations where the singleton pattern can come in handy.

### Now, let's take a look at a simple example of the singleton pattern in JavaScript:

```javascript
class Logger {
    constructor() {
        if (!Logger.instance) {
            Logger.instance = this;
            this.logs = [];
        }
        return Logger.instance;
    }

    log(message) {
        this.logs.push(message);
        console.log(message);
    }
}

const logger1 = new Logger();
const logger2 = new Logger();
logger1.log("Application started");
logger2.log("User logged in");
console.log(logger1.logs); // ["Application started", "User logged in"]
console.log(logger1 === logger2); // true
```

In this example, we've created a Logger class that has a constructor which checks if an instance property already exists on the class. If it doesn't, it creates one and assigns 'this' to it. If it does, it simply returns the existing instance.
The class also has a log method that adds a message to the logs array and logs it to the console.

When we create two instances of the Logger class, the constructor creates the instance property and logs array on the first instance, and then returns the first instance when we create the second instance. As a result, both logger1 and logger2 are the same object, and any logs added through either one will be added to the same logs array.

### Here's another example of the singleton pattern in JavaScript, this time with a "Configuration" class that stores application configuration options:

```javascript
class Configuration {
    constructor() {
        if (!Configuration.instance) {
            Configuration.instance = this;
            this.options = {};
        }
        return Configuration.instance;
    }

    setOption(key, value) {
        this.options[key] = value;
    }

    getOption(key) {
        return this.options[key];
    }
}

const config1 = new Configuration();
const config2 = new Configuration();
config1.setOption("language", "en");
config2.setOption("theme", "light");
console.log(config1.options); // {language: "en", theme: "light"}
console.log(config1 === config2); // true
```

In this example, we've created a Configuration class that has a constructor that works similarly to the previous example. The class also has setOption and getOption methods that allow you to set and get options respectively.

When we create two instances of the Configuration class, the constructor creates the instance property and options object on the first instance, and then returns the first instance when we create the second instance. As a result, both config1 and config2 are the same object, and any options set through either one will be added to the same options object.

### The examples above are for mutable instances. The instance can be immutable too. Here's an example of the singleton pattern in JavaScript, where the instance is immutable:

```javascript
class Singleton {
    constructor() {
        if (!Singleton.instance) {
            const instance = Object.freeze({});
            Singleton.instance = instance;
        }
        return Singleton.instance;
    }
}

const singleton1 = new Singleton();
singleton1.newProp = 'This should not work';
console.log(singleton1.newProp); // undefined

const singleton2 = new Singleton();
singleton2.newProp = 'This should not work either';
console.log(singleton2.newProp); // undefined
```

In this example, the Singleton class has a constructor that creates an instance property, but this time we use Object.freeze method to make it immutable. This method makes the object and all of its properties and methods non-writable, non-configurable, and non-enumerable.

When you try to add a new property to the instance, it will not work because the instance is immutable, and the property will not be added to it. This is shown by the console.log statement, which returns undefined for both instances.

This approach is useful when you want to prevent any unintended modifications to the singleton instance and make sure that it stays in a consistent state.

It's important to note that Object.freeze only makes the object itself immutable, any objects it references to will still be mutable. If you want to make the entire object graph immutable, you could use a library like seamless-immutable. 
