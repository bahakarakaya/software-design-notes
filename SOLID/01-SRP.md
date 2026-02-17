# Single Responsibility Principle

A class should have only one job; should fulfill a single, well defined responsibility.

As a commonly used definition, "***Every class should have only one reason to change***".  
*For example:* we have a **Barista** class with many functionalities such as `takeOrder`, `makeCoffee`, `calculateTax`, `cleanToilet`.

```Python
class Barista:
    def take_order(self, order):
        # some logic
        pass
    
    def make_coffee(self, order):
        # some logic
        pass

    def calculate_tax(self, order):
        # some logic
        pass

    def clean_toilet(self):
        # some logic
        pass
```

When we want to make a change in coffee making process, we update the **Barista** class. That's ok, right? Suppose we buy a new orange juice machine, change the payment device, add a new syrup etc. We have done a lot of updates in the class. As a result, the Barista class became bloated over time. We end up with a jack-of-all-trades 24 function multi utility Swiss Army knife that is trying to do everything. Hard to navigate and maintain, violates SRP.  

![alt text](images/srp1.png)

This is where we need **Separation of Concerns**:

* Coffee making process changes -> **Barista** is responsible.
* Salary or tax logic changes -> **Accountant** is responsible.
* Payment system changes -> **TransactionHandler** is responsible.

```Python
class Barista:
    def take_order(self, order):
        # some logic
        pass
    
    def make_coffee(self, order):
        # some logic
        pass


class Accountant:
    def calculate_salary(self, employee):
        # some logic
        pass

    def calculate_tax(self, employee):
        # some logic
        pass

    def pay_salary(self, employee):
        # some logic
        pass


class TransactionHandler:
    # some logic
    pass
```

For this reason, ***"Every class should have only one reason to change"***.

## Sources

- https://medium.com/@peterlee2068/software-design-principles-every-programmer-should-know-c164a83c6f87
- https://www.freecodecamp.org/news/solid-principles-single-responsibility-principle-explained/