## Evaluation criteria
- **Problem analysis** 
	- extract key entities and responsibilities
	- ask clarifying questions to lock down scope
	- frame the problem before touching code
- **Class Design**
	- choosing right responsibilities
	- shaping method signatures
	- defining clear ownership
	- keeping boundaries clean
- **Code Quality**
	- encapsulation
	- well-managed state
	- sensible use of composition or inheritance
	- clear separation of concerns
- **Extensibility and Maintainability**
	- Flexible structures with clean boundaries that can be expanded (for follow-ups)

# Delivery Framework
## 1. Requirements (5min)
-  **Primary capabilities** — What operations must this system support?
- **Rules and completion** — What conditions define success, failure, or when the system stops or transitions state?
- **Error handling** — How should the system respond when inputs or actions are invalid?
- **Scope boundaries** — What areas are _in_ scope (core logic, business rules) and what areas are explicitly _out_ (UI, storage, networking, concurrency, extensibility)?

## 2. Entities and Relationships (3min)
### 2.1 Identify entities
- Scan for things that need to exist in the system
Helpful filter:
- If something maintains changing state or enforces rules, it likely deserves to be its own entity.
- If it’s just information attached to something else, it’s probably just a field on another class.
### 2.2 Define relationships
- Which entity is the orchestrator — the one driving the main workflow?
- Which entities own durable state?
- How do they depend on each other? (has-a, uses, contains)
- Where should specific rules logically live?

## 3. Class design (10-15min)
For each entity, you'll answer two questions:
1. **State** - What does this class need to remember to enforce the requirements?
2. **Behaviour** - What does this class need to do, in terms of operations or queries?
### 3.1 Deriving State from Requirements
For each entity ask:
- Which parts of the requirements does this entity own?
- What information does it need to keep in memory to satisfy those responsibilities?
(e.g as it helps here)


For Tic Tac Toe, here's how this works for Game:

| Requirement                                              | What Game must track                                        |
| -------------------------------------------------------- | ----------------------------------------------------------- |
| "Two players alternate placing X and O on a 3x3 grid."   | The two players, whose turn it is, and the Board            |
| "The game ends when a player wins or the board is full." | Game state (in progress, won, draw) and the winner (if any) |

```
Game – State:
- board: Board
- playerX: Player
- playerO: Player
- currentPlayer: Player
- state: GameState (IN_PROGRESS, WON, DRAW)
- winner: Player? (null if no winner)
```


### Deriving Behaviour from requirements

for each class:
- What operations the outside world needs?
- Which requirements those operations statisfy?

For Tic Tac Toe, the requirements for Game translate to:

|Need from requirements|Method on Game|
|---|---|
|Players need to make moves|makeMove(player, row, col) returns bool|
|Ask whose turn it is|getCurrentPlayer() returns Player|
|Check game state|getGameState() returns GameState|
|See who won|getWinner() returns Player?|
|Inspect the board|getBoard() returns Board|

> [!NOTE]
> Keep rules with the entity that owns the relevant state (**Encapsulation** - "Tell, Don't Ask").
> 
> Objects should manage their own state and expose behaviour, not getters for callers to make decisions. 
> 
> Workflow and lifecycle rules ("can this operation run right now?") belong in the orchestrator, data specific rules ("is this cell occupied?") belong in the entity that owns that data.

Output from Class Design stage:
```
class Game:
  - board: Board
  - playerX: Player
  - playerO: Player
  - currentPlayer: Player
  - state: GameState (IN_PROGRESS, WON, DRAW)
  - winner: Player? (null if no winner)

  + makeMove(player, row, col) -> bool
  + getCurrentPlayer() -> Player
  + getGameState() -> GameState
  + getWinner() -> Player?
  + getBoard() -> Board
```


## 4. Implementation (10min)
- Check with interviewer what they prefer - full implementation or just pseudocode. Either way, focus on the most interesting methods first.

1. **Happy Path** -  walk through the method in a linear way, to show how the system actually moves
	1. Input it receives
	2. Sequence of steps it performs
	3. Internal calls it makes to other classes
	4. What it returns / How it changes state
2. **Edge Cases** - enumerate the failure modes to demonstrate production code thinking
	1. Invalid inputs
	2. Illegal operations
	3. Out-of-range values
	4. Calls that violate current system state
	5. Anything that must be rejected / Handled gracefully

- Often, interviewers will be explicit about which methods they want implemented.

### 4.1 Verification: Walk Through A Specific Scenario

- Spend 1-2 minutes to verify your logic by tracing through a concrete example. 
- Goal: try catching logical errors before interviewer finds them to demonstrate ability to verify your own code.

Pick a simple (but non-trivial) scenario and step through it, showing:
- Initial state
- What happens on each operation
- How state changes at each step
- Edge cases or transitions

Example:
```
Initial: board empty, currentPlayer = X
makeMove(X, 0, 0) → board[0][0] = X, currentPlayer = O
makeMove(O, 1, 1) → board[1][1] = O, currentPlayer = X
...
```


## 5. Extensibility (5min)
- Stay high level
- Goal is to demonstrate that initial design is extensible and robust.



# Design Principles

## General Software Design Principles

### KISS - keep it simple, stupid
- The simples solutions that works is usually the right one.
- The time to add complexity is when simplicity stops working

### DRY - Don't Repeat Yourself
- If logic is repeated in multiple places, pull it into one place.
- Don't go too far trying to merge similar but not identical functionalities
- Conflicts with KISS, as sometimes it is simpler to duplicate code rather than build an abstraction. The right move is to ==acknowledge both sides==
### YAGNI - You Aren't Gonna Need It
- Build what you need NOW, not what you might need later.
- Often guesses are wrong
- DO plan to extend but don't extend unless needed

### Separation of Concerns
- Different parts of code should handle different responsibilities and they shouldn't know about each other's internals.
- Makes it simpler to change how each component works without affecting others as long as the interfaces are consistent
- Example would be a function that renders board (GUI) and makes moves, etc.

### Law of Demeter (Principle of Least Knowledge)
- Method should talk to its immediate freinds and not reach through objects to access distant parts of the system
- Bad example: `order.getCustomer().getAddress().getZipCode()`
- Correct soln: put method `getCustomerZipCode()` in `Order` class and use that
- Method chaining is not issue as it returns and operates on the same object

## Object-Oriented Design Principles (SOLID)
### SRP - Single Responsibility Principle
- Class should have one reason to change. 
- If a class mixes multiple concerns - split them
- Example - report class that handles printing and saving

### OCP - Open/Closed Principle
- Support future requirements without modifying existing code
- Can be done by Abstract classes and interfaces
- If done correctly, new functionality becomes about writing new classes
- Example - PaymentProcessor class implementing methods vs PaymentMethod abstract class, then inherited by different methods

### LSP - Liskov Substitution Principle
- Subclasses must work wherever the base class works.
- Other words, subclass can add but not remove functionality of parent class
- Example - Bird class and Penguin class -> better is Bird -> Flying bird

### ISP - Interface Segregation Principle
- Small interfaces > large, general purpose interfaces
- Fat interfaces lead to many empty implementations, better to split these into smaller bits
- Example - Worker class (eat, sleep, work) and RobotWorker, which can only work!

### DIP - Dependency Inversion Principle
- Code should depend on abstractions, not concrete implementations
- Example - NotificationService should depend on abstract Sender class, and then can get passed a different sender based on needs (EmailSender, SMSSender, TestSender, etc)
- (this style described above is *dependency injection*)


**General Principles**

- KISS → Start simple, add complexity only when needed
- DRY → Reduce duplication, simplify maintenance
- YAGNI → Build for today, not hypothetical futures
- Separation of Concerns → Enable independent testing and changes
- Law of Demeter → Reduce coupling, hide internal structure

**SOLID Principles**

- SRP → Keep classes focused on one responsibility
- OCP → Support future requirements without modifying existing code
- LSP → Prevent brittle hierarchies that break at runtime
- ISP → Keep interfaces clean and focused
- DIP → Decouple business logic from implementation details


# OOP Concepts

## Encapsulation

- Keeping object's data private -> setters and getters
- In interview it is a basic hygiene check:
	- Do your classes expose their fields directly, or do they provide methods? 
	- Are you returning references to mutable internal collections that callers can modify, or are you returning copies?
- Example - Parking lot returning spots directly vs @property, etc;

## Abstraction

- Only expose what's essential and hide implementations details behind clear interfaces;
- In interviews - look for places where logic feels tangled or the requirements suggest multiple approaches (that would require ifs, enums, etc);
- Example - Order service uses payment API directly vs PaymentMethod class abstracting this interaction
- Hard part is choosing the right level of abstraction - too high -> meaningless interface (doWork, handeRequest), too specific -> nothing is abstracted

## Polymorphism

- Instead of checking types, let each object handle it itself;
- Example - parking lot carries mapping between vehicle type and size vs each object contains sizing
- Use polymorphism when behavior varies by type. If you see yourself writing type checks or switch statements on an enum, that's a sign you should be using polymorphism instead.

## Inheritance

- If one class is a more specific version of another, we can make one child of the other (e.g Bank Account -> Current Account)
- Con - causes very tight coupling, might be better to use composition + interfaces (abstract classes) (recommended for interviews)

## To sum up
- **Encapsulation**: Hide state, expose behavior. Make fields private, provide methods for access
- **Abstraction**: Define interfaces for variations. Multiple payment methods? Different vehicle types? Create an interface
- **Polymorphism**: Let objects handle themselves. No type checking, no switch statements on types
- **Inheritance**: Compose behavior, don't inherit it. Reach for interfaces first, use inheritance only when sharing stable implementation

