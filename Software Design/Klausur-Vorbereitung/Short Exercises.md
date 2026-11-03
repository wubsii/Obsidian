Try each one without looking anything up, then compare with your class notes. Each exercise is small enough to fit in one file, and all of them use a `main` method so you can run it and see the output.

### 1. Strategy: Duck flying

Create a `FlyBehavior` interface with a `fly()` method, and two implementations: `FlyWithWings` and `FlyNoWay`. Create a `Duck` class that holds a `FlyBehavior`, has a `performFly()` method, and a `setFlyBehavior()` setter. In `main`, make a duck that flies with wings, then swap it to `FlyNoWay` at runtime and call `performFly()` again.

### 2. Template Method: Caffeine drinks

Create an abstract class `CaffeineBeverage` with a `final` method `prepareRecipe()` that calls `boilWater()`, `brew()`, `pourInCup()`, and `addCondiments()`. Implement `boilWater` and `pourInCup` in the base class and make `brew` and `addCondiments` abstract. Create `Tea` and `Coffee` subclasses and run both from `main`.

### 3. Observer: Weather station

Create `Subject` and `Observer` interfaces. `Subject` has `registerObserver`, `removeObserver` and `notifyObservers`; `Observer` has `update(float temperature)`. Build a `WeatherStation` that stores observers in a list and a `PhoneDisplay` and `WindowDisplay` that print the temperature on update. In `main`, register both, change the temperature, then remove one and change it again.

Create a `Command` interface with `execute()` and `undo()`. Create a `Light` receiver with `on()` and `off()`, plus `LightOnCommand` and `LightOffCommand`. Create a `RemoteControl` invoker with a few button slots and a `Deque<Command>` history, a `pressButton(int slot)` method and an `undo()` method that pops the last command.

### 5. Singleton: Thread-safe settings manager

Create a `SettingsManager` class with a private constructor, a private static instance, and a `synchronized` static `getInstance()`. Add a `volume` field with getter and setter. In `main`, start two threads that both call `getInstance()` and print `System.identityHashCode` of what they get, to prove it's the same object.

### 6. Factory: Enemy creator

Create an `Enemy` interface with `attack()`, and `Orc`, `Goblin` and `Dragon` classes. Create an `EnemyFactory` with a method `createEnemy(String type)` that returns the right one. In `main`, ask the factory for three enemies by name and call `attack()` on each, without ever writing `new Orc()` outside the factory.

### 7. Adapter: Turkey as duck

Create `Duck` (with `quack()` and `fly()`) and `Turkey` (with `gobble()` and `fly()`). Write a `TurkeyAdapter` that implements or extends `Duck` (whichever your class used), holds a `Turkey`, and maps `quack()` to `gobble()`. Test it by passing the adapter into a method that expects a `Duck`.

### 8. Facade: Home theater

Create small classes `Projector`, `SoundSystem` and `Lights`, each with a couple of print-only methods. Write a `HomeTheaterFacade` with `watchMovie()` and `endMovie()` that call the right methods on all three in the right order. In `main`, only talk to the facade.

### 9. Decorator: Coffee shop

Create a `Beverage` abstract class with `getDescription()` and `cost()`. Create `Espresso` as a concrete beverage. Create a `CondimentDecorator` that extends `Beverage` and holds a `Beverage`, then `Milk` and `Caramel` decorators that add to the description and the cost. In `main`, wrap an espresso in milk and then caramel, and print the final description and price.

### 10. Iterator: Combined menu

Create a `MenuItem` class with name and price. Create `BreakfastMenu` that stores items in an array and `LunchMenu` that stores them in an `ArrayList`. Each should have a method that returns an `Iterator<MenuItem>`. Write one `printMenu(Iterator<MenuItem>)` method and use it for both menus.

## Part 3: Stretch challenges

Once the ten above work, try combining them.

- **Undoable editor:** build the text editor from earlier with a `Document` receiver, `TypeCommand` and `DeleteCommand`, and a toolbar with undo and redo (two stacks).
- **Observer plus Singleton:** make the weather station a singleton and have displays register themselves.
- **Decorator plus Factory:** write a `BeverageFactory` that builds a drink from a string like `"espresso+milk+caramel"`.
- **Strategy plus Template:** a `Character` class that holds a swappable weapon strategy, and a template method `takeTurn()` with the fixed steps scan, choose, act, end turn.

Tip: after each one, write a single sentence explaining which pattern you used and why, because that's exactly what an exam answer needs.