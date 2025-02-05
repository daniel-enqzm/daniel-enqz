# OOP 🤔


### Analyzing the right way

|Diagram Type | Description |
|-------------|-------------|
|Class diagrams| Show the classes, objects, and relationships between them in a system, including attributes and methods of each class.|
|Sequence diagrams| Show the interactions between objects over time, including the order of messages and the objects that initiate and receive them.|
|State diagrams| Show the states of an object over time, including the conditions that trigger changes in state and the actions that occur in response.|
|Use case diagrams| Show the relationships between actors and use cases, which are high-level descriptions of a system's functions and features.|

### Basics

| Concept | Definition | Usage |
| --- | --- | --- |
| Classes and Objects | Class is a blueprint for creating objects, objects are instances of classes | Athlete&nbsp;class defines attributes and methods;&nbsp;footballer&nbsp;and&nbsp;basketballer&nbsp;are object instances. |
| Inheritance | When classes inherit behavior and state from parent class | Footballer&nbsp;and&nbsp;Basketballer&nbsp;inherit properties and methods from&nbsp;Athlete. |
| Encapsulation | Hiding the implementation details of a class from the outside world, using private or read/write methods. | Attributes are private; accessed via getter/setter methods (especially in Java version). |
| Abstraction | Is about simplifying complex systems by modeling classes based on the essential properties and behaviors. | Athlete&nbsp;class defines abstract&nbsp;play()&nbsp;method, hiding implementation details. |
| Polymorphism | It's when objects of different types can be accessed through the same interface. | play()&nbsp;method behaves differently for&nbsp;Footballer&nbsp;and&nbsp;Basketballer, despite same method name. |

```ruby
class Athlete
  attr_reader: :name, :sport
  attr_writer: :heigth

  def initialize(name, sport, heigth)
    @name = name
    @sport = sport
    @heigth = heigth
  end

  def play
    raise "Must be implemented in subclass"
  end
end

def Footballer < Athlete
  def play
    puts "Im playing #{sport}"
  end
end

def Basketballer < Athlete
  def play
    puts "Im playing #{sport}"
  end
end

footballer = Footballer.new("Messi", "Football", 1.7)
basketballer = Basketballer.new("Lebron", "Basketball", 2.0)

p footballer.play # Im playing football
p basketballer.play # Im playing basketball

p footballer.name # Messi
p basketballer.name # Lebron

basketballer.heigth = 2.1
p basketballer.heigth # 2.1
```

## Design Principles

### Essentials 👆
| Acronym | Definition |
| --- | --- |
| DRY | Dont Repeat Yourself |
| YAGNI | You aint gonna need it |
| KISS | Keep it Simple, Stupid |


### About SOLID 🌊
| Concept | Definition |
| --- | --- |
| Single Responsibility Principle | A class should have only one reason to change. |
| Open/Closed Principle | A class should be open for extension but closed for modification. |
| Liskov Substitution Principle | Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program. |
| Interface Segregation Principle | Many client-specific interfaces are better than one general-purpose interface. |
| Dependency Inversion Principle | Depend upon abstractions. Do not depend upon concrete classes. |



### Examples 📘

> (SRP) In the next example the class `User` has one main responsibility, which is to save the user to the database. <br>
> (OCP) We can extend the class `User` to create a new class `Admin` and override the method `save` to save the admin to the database. <br>
> (ISP) We are adding the interface send_email only to admins and not to users. This is because the Users don't need to send emails. <br>

```ruby
module EmailSender
  def send_email
    # code to send email
  end
end

class User
  def initialize(name, email, password)
    @name = name
    @email = email
    @password = password
  end

  def save
    # save user to database
  end
end

class Admin < User
  include EmailSender

  def initialize(name, email, password)
    super(name, email, password)
  end

  def save
    super
    # save admin to database
  end
end
```

>(LSP) In the next example we have a Penguin and Bird class, the Penguin class inherits from the Bird class. The Penguin class is a subtype of the Bird class. The Bird class method can be replaced with the Penguin one, without altering the correctness of the program.

```ruby
class Bird
  def fly
    puts "I am flying!"
  end
end

class Penguin < Bird
  def fly
    puts "Sorry, I cannot fly. I am a penguin."
  end
end

def test_bird_flight(bird)
  bird.fly
end

bird = Bird.new
penguin = Penguin.new

test_bird_flight(bird) # Output: "I am flying!"
test_bird_flight(penguin) # Output: "Sorry, I cannot fly. I am a penguin."
```

>(DIP) In the next example, the High Level module UserService depends on an abstaction (an instance of the low level UserRepository) and not directly on the User Repository.
```ruby
# High level module
class UserService
  def initialize(user_repository)
    @user_repository = user_repository
  end

  def get_user(id)
    @user_repository.find(id)
  end
end

# Low-level module
class UserRepository
  def find(id)
    # database query to fetch user
  end
end

# Client code
user_repository = UserRepository.new
user_service = UserService.new(user_repository)
user = user_service.get_user(1)

```
