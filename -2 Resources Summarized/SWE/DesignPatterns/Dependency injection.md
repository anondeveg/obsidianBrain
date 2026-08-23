
Dependecy injection is a design pattern where an object recives its dependecies instead of creating it itself.

there is 3 types of dependecy injection.
# types of dependecy injection
##  Constructor Injection
With Constructor Injection, dependencies are provided to a class through its constructor when the object is created. This is the most common form of DI because it makes dependencies clear, mandatory, and immutable after the object is constructed.

```py
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self, engine):
        self.engine = engine  # Declaring a dependency on Engine

    def drive(self):
        self.engine.start()  # Using the injected Engine dependency
        print("Car is driving")

# Main execution
engine = Engine()  # Create Engine object (dependency)

# Injecting Engine dependency when creating Car
car = Car(engine)  # Pass the Engine instance to the constructor
car.drive()  # Call the drive method to use the Engine
```

## 2. Setter Injection

```py
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = None  # Declaring a dependency on Engine

    # No constructor injection here. Using setter to inject dependency
    def set_engine(self, engine):
        self.engine = engine  # Injecting dependency via setter method

    def drive(self):
        self.engine.start()  # Using the injected Engine dependency
        print("Car is driving")

# Create Engine object (dependency)
engine = Engine()

# Create a Car object without providing the Engine immediately
car = Car()

# Inject the Engine dependency using the setter method
car.set_engine(engine)  # Set the dependency via the setter method
car.drive()  # Call the drive method to use the Engine
```

## 3. Interface Injection
```
class Engine:
    def start(self):
        print("Engine started")

# Define an interface for injecting dependencies
class EngineInjector:
    def inject_engine(self, engine):
        pass  # Method to inject the Engine dependency

class Car(EngineInjector):
    def __init__(self):
        self.engine = None  # Declaring a dependency on Engine

    # Implement the injectEngine method to set the Engine dependency
    def inject_engine(self, engine):
        self.engine = engine  # Dependency injected through the interface method

    def drive(self):
        self.engine.start()  # Using the injected Engine dependency
        print("Car is driving")

if __name__ == "__main__":
    engine = Engine()  # Create Engine object (dependency)

    car = Car()  # Create Car object
    car.inject_engine(engine)  # Inject dependency via the inject_engine() method
    car.drive()  # Call the drive method to use the Engine
```

# why use it?
- improved testability: easily inject mocks or test doubles to test components in isolation.
-  cross-cutting concerns: conveniently inject services like logging, security, or caching across multiple components.
