## 5 Principles to write SOLID Code

>SOLID is the acronym for a collection of 
> 5 object-oriented design principles, 
> first conceptualised 
> by Robert C. Martin

> They are meant to help creating simpler, 
> more easily understandable, 
> maintainable and expandable code

The letters stand for:
- [1> Single Responsibility Principle] (#1-single-responsibility-principle)
- 2> Open/Closed Principle
- 3> Liskov Substitution Principle
- 4> Interface Segregation Principle
- 5> Dependency Inversion Principle

## 1. Single Responsibility Principle
> A class should have one, and only one, reason to change.

```python
class Animal:
    def __init__(self, name: str):
        self.name = name
    
    def get_name(self) -> str:
        pass

    def save(self, animal):
        pass
```

```python
class Animal:
    def __init__(self, name: str):
            self.name = name
    
    def get_name(self):
        pass


class AnimalDB:
    def get_animal(self) -> Animal:
        pass

    def save(self, animal: Animal):
        pass
```

## 2. Open/Closed Principle
> Software entities (classes, modules, functions, etc.) 
> should be open for extension, but closed for modification.

```python
class Connection:
    def get_connection(self, connect: str):
        if connect == 'SqlServer':
            print("Connect with SqlServer")
            pass

        if connect == 'MySqlServer':
            print("Connect with MySqlServer")
            pass
```

```python
class Connection:
    def get_connection(self):
        pass


class SqlServer(Connection):
    def get_connection(self):
        # Connect with SqlServer
        print("Connect with SqlServer")
        pass


class MySqlServer(Connection):
    def get_connection(self):
        # Connect with MySqlServer
        print("Connect with MySqlServer")
        pass
```

## 3. Liskov Substitution Principle
>The principle defines that objects of a superclass 
> shall be replaceable with objects of 
> its subclasses without breaking the application

```python
from abc import ABC, abstractmethod


class Employee(ABC):
    @abstractmethod
    def working(self):
        pass

    @abstractmethod
    def checkAttendance(self):
        pass


class Developer(Employee):
    def working(self):
        pass

    def checkAttendance(self):
        pass


class CleanStaff(Employee):
    def working(self):
        pass

    def checkAttendance(self):
        raise Exception
```

```python
from abc import ABC, abstractmethod


class Employee(ABC):
    @abstractmethod
    def working(self):
        pass


class CheckAttendance(ABC):
    @abstractmethod
    def checkAttendance(self):
        pass

    
class Developer(Employee, CheckAttendance):
    def working(self):
        pass

    def checkAttendance(self):
        pass
    
    
class CleanStaff(Employee):
    def working(self):
        pass

```

## 4. Interface Segregation Principle
>Clients should not be forced to depend 
> upon interfaces that they do not use

```python
from abc import ABC, abstractmethod


class Animal(ABC):
    @abstractmethod
    def eat(self):
        pass

    @abstractmethod
    def fly(self):
        pass
    
    @abstractmethod
    def run(self):
        pass
        

class Snake(Animal):
    def eat(self):
        pass

    def fly(self):
        pass
    
    def run(self):
        pass

```


```python
from abc import ABC, abstractmethod


class Animal(ABC):
    @abstractmethod
    def eat(self):
        pass


class Snake(Animal):
    def eat(self):
        pass

    def crawl(self):
        pass


class Dog(Animal):
    def eat(self):
        pass

    def run(self):
        pass

```

## 5. Dependency Inversion Principle

>High-level modules should not depend on low-level modules. 
> Both should depend on abstractions (e.g. interfaces).
> 
>Abstractions should not depend on details. 
> Details (concrete implementations) should depend on abstractions

```python
from abc import ABC, abstractmethod


class ConnectionOld:
    def get_connection(self, conn):
        if conn == 'SqlServer':
            # Connect with SqlServer
            print("Connect with SqlServer")
            return

        if conn == 'MySqlServer':
            # Connect with MySql
            print("Connect with MySqlServer")
            return


class Connection(ABC):
    @abstractmethod
    def get_connection(self):
        pass


class SqlServer(Connection):
    def get_connection(self):
        # Connect with SqlServer
        print("Connect with SqlServer")
        return


class MySqlServer(Connection):
    def get_connection(self):
        # Connect with MySqlServer
        print("Connect with MySqlServer")
        return


class ConnectionManager:
    def __init__(self, connection):
        self.connection = connection

    def get_connection(self):
        return self.connection.get_connection()


if __name__ == '__main__':
    conn = ConnectionManager(
        MySqlServer()
    ).get_connection()

    print(conn)
```

## Conclusion
> The **SOLID** design principles are meant to be a guideline to 
> write maintainable, expandable and easy to understand code.