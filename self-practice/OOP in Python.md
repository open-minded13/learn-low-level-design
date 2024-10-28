# Object-Oriented Programming (OOP) in Python

Object-Oriented Programming (OOP) is a programming paradigm that uses "objects" and their interactions to design and program applications. Python, being an object-oriented language, allows you to leverage OOP concepts to write clean, efficient, and reusable code.

This tutorial covers the four main principles of OOP:

- **Encapsulation**
- **Inheritance**
- **Polymorphism**
- **Abstraction**

We'll explore each concept with practical examples, clarifications, and exercises to help you gain a solid understanding.

---

## Table of Contents

1. [Classes and Objects](#1-classes-and-objects)
2. [Encapsulation](#2-encapsulation)
3. [Inheritance](#3-inheritance)
4. [Polymorphism](#4-polymorphism)
5. [Abstraction](#5-abstraction)
6. [Pizza Price Calculator Exercise](#6-pizza-price-calculator-exercise)

---

## 1. Classes and Objects

A **class** is a blueprint for creating objects (instances). An **object** is an instance of a class. Classes encapsulate data (attributes) and functions (methods) that operate on the data.

### Example

```python
# Define a class
class Car:
    def __init__(self, make, model):
        self.make = make
        self.model = model
    
    def display_info(self):
        print(f"Car make: {self.make}, model: {self.model}")

# Create an object from the Car class
my_car = Car("Toyota", "Corolla")
my_car.display_info()
```

**Explanation:**

- The `Car` class has two attributes: `make` and `model`.
- The `__init__` method initializes these attributes when a new object is created.
- The `display_info` method prints the car's details.
- We create an instance `my_car` of the `Car` class and call `display_info()`.

---

### Exercise

**Task:**

1. Create a class named `Person` with attributes `name` and `age`.
2. Add a method `greet` that prints a greeting message including the person's name.
3. Create an instance of `Person` and call the `greet` method.

**Practice Code:**

```python
# Your code here
```

---

### Solution

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        print(f"Hello! My name is {self.name} and I am {self.age} years old.")

# Example usage
person = Person("Alice", 30)
person.greet()
```

---

## 2. Encapsulation

**Encapsulation** is the concept of bundling data (attributes) and methods that operate on that data within one unit (class). It restricts direct access to some of an object's components, which is a way of preventing accidental or unauthorized manipulation of data.

In Python, attributes are public by default. However, you can indicate that an attribute should be treated as private by prefixing it with double underscores `__`.

### Example

```python
class BankAccount:
    def __init__(self, account_number, balance):
        self.__account_number = account_number  # Private attribute
        self.__balance = balance                # Private attribute

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient funds")

    def get_balance(self):
        return self.__balance

# Example usage
account = BankAccount("123456", 1000)
account.deposit(500)
account.withdraw(200)
print(f"Balance: ${account.get_balance()}")

# Attempting to access private attributes
# print(account.__balance)  # Raises AttributeError
```

**Explanation:**

- `__account_number` and `__balance` are private attributes due to the double underscores.
- Methods `deposit`, `withdraw`, and `get_balance` provide controlled access to `__balance`.
- Attempting to access `__balance` directly will result in an `AttributeError`.

---

### Exercise

**Task:**

1. Create a class `LibraryBook` with private attributes `__title` and `__author`.
2. Add a method `display_info` to show the book's information.
3. Add a method `borrow` to change the book's availability status.
4. Try to access the private attributes directly and observe what happens.

**Practice Code:**

```python
# Your code here
```

---

### Solution

```python
class LibraryBook:
    def __init__(self, title, author):
        self.__title = title           # Private attribute
        self.__author = author         # Private attribute
        self.__is_borrowed = False     # Private attribute

    def display_info(self):
        print(f"Title: {self.__title}, Author: {self.__author}")

    def borrow(self):
        if not self.__is_borrowed:
            self.__is_borrowed = True
            print("Book borrowed.")
        else:
            print("Book is already borrowed.")

# Example usage
book = LibraryBook("1984", "George Orwell")
book.display_info()
book.borrow()
book.borrow()  # Attempt to borrow again

# Attempting to access private attributes
# print(book.__title)  # Raises AttributeError
```

**Note:** Even with name mangling, you can access the private attributes using `_ClassName__attribute`, but this is discouraged.

```python
# Accessing mangled private attribute (not recommended)
print(book._LibraryBook__title)  # Outputs: 1984
```

---

## 3. Inheritance

**Inheritance** allows a class (child class) to inherit attributes and methods from another class (parent class). This promotes code reuse and logical hierarchy.

### Example

```python
# Parent class
class Vehicle:
    def __init__(self, color):
        self.color = color

    def show_color(self):
        print(f"Color: {self.color}")

# Child class
class Car(Vehicle):
    def __init__(self, color, brand):
        super().__init__(color)  # Calls the parent class's __init__ method
        self.brand = brand

    def display_info(self):
        print(f"Brand: {self.brand}, Color: {self.color}")
```

**Explanation:**

1. **Does `class Car(Vehicle)` mean it inherits from the class `Vehicle`? Why does `class Vehicle` not need parentheses?**

   - Yes, `class Car(Vehicle)` means `Car` inherits from `Vehicle`.
   - `Vehicle` does not inherit from any other class, so it doesn't need parentheses. By default, all classes in Python inherit from `object` if no parent class is specified.

2. **What is the meaning of `super()` in the line `super().__init__(color)`?**

   - `super()` returns a temporary object of the parent class (`Vehicle` in this case) and allows you to call its methods.
   - `super().__init__(color)` calls the `__init__` method of the parent class to initialize the `color` attribute. This avoids code duplication and ensures that the parent class is properly initialized.

3. **Why does `def show(self)` in the class `PDF(Document)` not need `super()` compared to the previous case (`super().__init__(color)`)?

   - In the `PDF` class, if the `show` method does not need to extend or call the parent class's `show` method, you don't need to use `super()`.
   - If you're overriding a method and don't need to use any functionality from the parent method, you can simply redefine it without calling `super()`. However, if you want to extend the parent method's behavior, you can call `super().method_name()`.

### Example Usage

```python
# Create an instance of Car
my_car = Car("Red", "Toyota")
my_car.display_info()
```

**Output:**

```
Brand: Toyota, Color: Red
```

---

### Exercise

**Task:**

1. Create a base class `Animal` with a method `make_sound` and an attribute `species`.
2. Create a subclass `Dog` that inherits from `Animal`.
3. In `Dog`, override the `make_sound` method to print `"Woof"`.
4. Add an additional method `fetch` in `Dog`.

**Practice Code:**

```python
# Your code here
```

---

### Solution

```python
# Parent class
class Animal:
    def __init__(self, species):
        self.species = species

    def make_sound(self):
        print("Some generic animal sound.")

# Child class
class Dog(Animal):
    def __init__(self, species):
        super().__init__(species)

    def make_sound(self):
        print("Woof")

    def fetch(self):
        print("Dog is fetching the ball.")

# Example usage
dog = Dog("Canine")
dog.make_sound()  # Outputs: Woof
dog.fetch()       # Outputs: Dog is fetching the ball.
```

---

## 4. Polymorphism

**Polymorphism** allows methods to do different things based on the object they are acting upon, even if they share the same name. It provides a way to perform a single action in different forms.

### Example

```python
class Bird:
    def sound(self):
        print("Chirp")

class Cat:
    def sound(self):
        print("Meow")

class Dog:
    def sound(self):
        print("Woof")

# Polymorphism in action
animals = [Bird(), Cat(), Dog()]
for animal in animals:
    animal.sound()
```

**Output:**

```
Chirp
Meow
Woof
```

**Explanation:**

- Each class (`Bird`, `Cat`, `Dog`) has a `sound` method.
- We can call `sound` on any animal without knowing its exact type.

---

### Exercise

**Task:**

1. Create a base class `Shape` with a method `area`.
2. Create two subclasses `Circle` and `Rectangle`.
3. In `Circle`, implement `area` to calculate the area of a circle.
4. In `Rectangle`, implement `area` to calculate the area of a rectangle.
5. Demonstrate polymorphism by creating a list of shapes and calling `area` on each.

**Practice Code:**

```python
# Your code here
```

---

### Solution

```python
import math

class Shape:
    def area(self):
        pass  # Empty method

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

# Example usage
shapes = [Circle(5), Rectangle(4, 6)]
for shape in shapes:
    print(f"Area: {shape.area()}")
```

**Output:**

```
Area: 78.53981633974483
Area: 24
```

---

## 5. Abstraction

**Abstraction** is the concept of hiding complex implementation details and showing only the necessary features of an object. It helps in reducing programming complexity and effort.

In Python, we can achieve abstraction using abstract base classes (ABCs) provided by the `abc` module.

### Example

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

class Car(Vehicle):
    def start_engine(self):
        print("Car engine started.")

class Motorcycle(Vehicle):
    def start_engine(self):
        print("Motorcycle engine started.")
```

**Explanation:**

1. **Why do we need a class `Shape(ABC)` with an `abstractmethod`? What is the difference if we don't use them?**

   - An abstract base class (ABC) is a class that cannot be instantiated and typically includes one or more abstract methods that must be implemented by subclasses.
   - Using an abstract class enforces that any subclass must implement the abstract methods, providing a consistent interface.
   - If we don't use an abstract class, subclasses may forget to implement critical methods, leading to runtime errors.
   - Abstract classes promote code consistency and help catch errors early in the development process.

2. **Better Example:**

   - Let's consider a `Payment` system where different payment methods must implement a `process_payment` method.

```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def process_payment(self, amount):
        pass

class CreditCardPayment(Payment):
    def process_payment(self, amount):
        print(f"Processing credit card payment of ${amount}")

class PayPalPayment(Payment):
    def process_payment(self, amount):
        print(f"Processing PayPal payment of ${amount}")

# Attempting to instantiate Payment
# payment = Payment()  # Raises TypeError

# Using the subclasses
payment1 = CreditCardPayment()
payment1.process_payment(100)

payment2 = PayPalPayment()
payment2.process_payment(150)
```

**Explanation:**

- The `Payment` class is an abstract base class with an abstract method `process_payment`.
- Subclasses `CreditCardPayment` and `PayPalPayment` implement the `process_payment` method.
- Attempting to instantiate `Payment` directly raises a `TypeError`.

---

### Exercise

**Task:**

1. Create an abstract class `Appliance` with an abstract method `turn_on`.
2. Create subclasses `WashingMachine` and `Refrigerator` that inherit from `Appliance`.
3. Implement the `turn_on` method in each subclass with appropriate messages.
4. Try to instantiate `Appliance` and observe what happens.

**Practice Code:**

```python
# Your code here
```

---

### Solution

```python
from abc import ABC, abstractmethod

class Appliance(ABC):
    @abstractmethod
    def turn_on(self):
        pass

class WashingMachine(Appliance):
    def turn_on(self):
        print("Washing machine is now running.")

class Refrigerator(Appliance):
    def turn_on(self):
        print("Refrigerator is now cooling.")

# Example usage
washer = WashingMachine()
washer.turn_on()  # Outputs: Washing machine is now running.

fridge = Refrigerator()
fridge.turn_on()  # Outputs: Refrigerator is now cooling.

# Attempt to instantiate Appliance
# appliance = Appliance()  # Raises TypeError
```

**Explanation:**

- Attempting to instantiate `Appliance` results in a `TypeError` because it contains abstract methods.
- This enforces that only fully implemented subclasses can be instantiated.

---

## 6. Pizza Price Calculator Exercise

Let's apply the OOP concepts we've learned in a practical exercise.

**Question:**

Write a program to calculate the price of a pizza based on its size and selected toppings.

**Requirements:**

1. **Pizza Sizes:**

   - **Small**: \$5.00
   - **Medium**: \$7.00
   - **Large**: \$10.00

2. **Available Toppings and Prices:**

   - Cheese: \$1.50
   - Tomatoes: \$0.75
   - Onions: \$0.50
   - Peppers: \$0.70
   - Mushrooms: \$1.25
   - Bacon: \$2.00

3. **Implement a `Pizza` class that:**

   - Takes a base pizza with a specified size.
   - Allows adding toppings to the pizza.
   - Calculates the total price using a `get_price()` method.

4. **Design Patterns:**

   - **Primary Approach:** Use the **Decorator Design Pattern**, where each topping is a decorator that wraps a pizza object.
   - **Alternative Approach:** Use a **Dictionary** to store topping prices and calculate the total price.

**Example Usage:**

- **Input:**

  ```python
  size = "Medium"
  toppings = ["Cheese", "Tomatoes", "Onions"]
  ```

- **Expected Output:**

  ```
  Base Price (Medium): $7.00
  Cheese: $1.50
  Tomatoes: $0.75
  Onions: $0.50
  Total Price: $9.75
  ```

---

### Solution

#### **Decorator Design Pattern Solution**

```python
from abc import ABC, abstractmethod

# Abstract Pizza Component
class Pizza(ABC):
    @abstractmethod
    def get_price(self):
        pass

# Concrete Pizza Component
class BasePizza(Pizza):
    size_prices = {"Small": 5.00, "Medium": 7.00, "Large": 10.00}

    def __init__(self, size):
        self.size = size

    def get_price(self):
        return self.size_prices.get(self.size, 0)

# Abstract Topping Decorator
class ToppingDecorator(Pizza):
    def __init__(self, pizza):
        self.pizza = pizza

    @abstractmethod
    def get_price(self):
        pass

# Concrete Toppings
class Cheese(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 1.50

class Tomatoes(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 0.75

class Onions(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 0.50

class Peppers(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 0.70

class Mushrooms(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 1.25

class Bacon(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 2.00

# Example usage
def main():
    pizza = BasePizza("Medium")
    pizza = Cheese(pizza)
    pizza = Tomatoes(pizza)
    pizza = Onions(pizza)
    total_price = pizza.get_price()
    print(f"Total Pizza Price: ${total_price:.2f}")

if __name__ == "__main__":
    main()
```

---

#### **Alternative Solution Using Dictionary**

```python
class Pizza:
    size_prices = {"Small": 5.00, "Medium": 7.00, "Large": 10.00}
    topping_prices = {
        "Cheese": 1.50,
        "Tomatoes": 0.75,
        "Onions": 0.50,
        "Peppers": 0.70,
        "Mushrooms": 1.25,
        "Bacon": 2.00
    }

    def __init__(self, size):
        self.size = size
        self.toppings = []

    def add_topping(self, topping):
        if topping in self.topping_prices:
            self.toppings.append(topping)
        else:
            print(f"Error: '{topping}' is not an available topping.")

    def get_price(self):
        total_price = self.size_prices.get(self.size, 0)
        for topping in self.toppings:
            total_price += self.topping_prices[topping]
        return total_price

# Example usage
def main():
    pizza = Pizza("Medium")
    pizza.add_topping("Cheese")
    pizza.add_topping("Tomatoes")
    pizza.add_topping("Onions")
    total_price = pizza.get_price()
    print(f"Total Pizza Price: ${total_price:.2f}")

if __name__ == "__main__":
    main()
```

---

### Exercise

**Task:**

1. **Extend the Decorator Pattern:**

   - Add toppings `Olives` (\$0.90) and `Chicken` (\$2.50).
   - Implement their classes similar to other toppings.

2. **Enhance the Dictionary Approach:**

   - Modify `add_topping` to return `True` if successful and `False` otherwise.
   - Handle unavailable toppings gracefully.

**Practice Code:**

```python
# For Decorator Pattern
# Your code here

# For Dictionary Approach
# Your code here
```

---

### Solution

#### Decorator Pattern

```python
class Olives(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 0.90

class Chicken(ToppingDecorator):
    def get_price(self):
        return self.pizza.get_price() + 2.50

# Example usage
def main():
    pizza = BasePizza("Large")
    pizza = Cheese(pizza)
    pizza = Olives(pizza)
    pizza = Chicken(pizza)
    total_price = pizza.get_price()
    print(f"Total Pizza Price: ${total_price:.2f}")

if __name__ == "__main__":
    main()
```

#### Dictionary Approach

```python
class Pizza:
    # ... (same as before)
    topping_prices = {
        "Cheese": 1.50,
        "Tomatoes": 0.75,
        "Onions": 0.50,
        "Peppers": 0.70,
        "Mushrooms": 1.25,
        "Bacon": 2.00,
        "Olives": 0.90,
        "Chicken": 2.50
    }

    def add_topping(self, topping):
        if topping in self.topping_prices:
            self.toppings.append(topping)
            return True
        else:
            print(f"Error: '{topping}' is not an available topping.")
            return False

# Example usage
def main():
    pizza = Pizza("Large")
    success = pizza.add_topping("Pineapple")
    if not success:
        print("Please choose an available topping.")
    pizza.add_topping("Olives")
    pizza.add_topping("Chicken")
    total_price = pizza.get_price()
    print(f"Total Pizza Price: ${total_price:.2f}")

if __name__ == "__main__":
    main()
```

---

**Discussion:**

- The **Decorator Pattern** is more flexible and scalable, allowing easy addition of new toppings without modifying existing code.
- The **Dictionary Approach** is simpler and more efficient for quick calculations but may become cumbersome as complexity increases.

---

## Conclusion

In this tutorial, we've explored the fundamental concepts of Object-Oriented Programming in Python, including classes and objects, encapsulation, inheritance, polymorphism, and abstraction. We've applied these concepts through practical examples and exercises to reinforce learning.

By understanding and practicing these principles, you'll be better equipped to write modular, reusable, and maintainable code in Python.
