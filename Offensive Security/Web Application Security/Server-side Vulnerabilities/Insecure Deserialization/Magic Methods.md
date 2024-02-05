Magic methods are a special subset of methods and a common feature of OOP, usually indicated by prefixing or surrounding the method with double underscores.

Magic methods don't need to be explicitly invoke, instead they are automatically invoked whenever a particular event or scenario occurs. Developers usually add magic methods to a class to predetermine what code should be executed when the corresponding event or scenario occurs.

Common examples of magic methods are PHP's `__construct()` and Python's `__init__`, which is invoked whenever the class is instantiated. These type of magic methods are called constructors, and they typically contain code to initialize attributes of the class instance.

Magic methods are generally safe, however, they can become dangerous when the code they execute handles user-controllable data, for example, from a deserialized object. This can be exploited by an attacker to automatically invoke methods on the deserialized data when the corresponding conditions are met.

Some languages have magic methods that are automatically invoked during the serialization and deserialization process. For example, the PHP's `serialize()` and `unserialize()` method looks for and invokes an object's `__sleep()` and `__wakeup()` magic methods, respectively.