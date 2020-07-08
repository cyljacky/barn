---
description: >-
  Without violating encapsulation, capture and externalize an object’s internal
  state so that the object can be restored to this state later.
---

# Memento Pattern

## Features

* Store the historical state of the object which can be retrieved later
* The historical state cannot be modified
* Undo / redo

## Characters

* **Originator**:
  * creates a Memento to store the internal state;
  * uses Mementos to restore its state;
* **Memento**:
  * stores an immutable snapshot of the internal state of Originator;
  * can be accessed _only_ by the Originator;
* **Caretaker**:
  * stores Mementos;
  * never operates on or read Mementos;

```text
// Originator
class Calculator {
    private string display;

    private power(string expression): number;
    
    setState(string display): void;
    calculate(): number;
    save(): Snapshot;
    restore(Snapshot snapshot): void; 
}

// Memento
class Snapshot {
    private string state;

    getState(): state;
}

// CareTaker
class Application {
    Calculator calculator;
    Array<Snapshot> undoSnapshots;
    Array<Snapshot> redoSnapshots;

    calculate(): void {
        const snapshot = this.calculator.save()
        this.undoSnapshots.push(snapshot)
        this.redoSnapshots = []
        this.calculator.calculate()
    }

    undo(): void {
        const snapshot = this.undoSnapshots.pop()
        this.redoSnapshots.push(snapshot)
        this.calculator.restore(snapshot)
    }

    redo(): void {
        const snapshot = this.redoSnapshots.pop()
        this.undoSnapshots.push(snapshot)
        this.calculator.restore(snapshot)
    }
}
```

## Reference

{% embed url="https://withbenefits.dev/design-patterns-memento/" %}





