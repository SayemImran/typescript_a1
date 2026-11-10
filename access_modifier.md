# TypeScript Access Modifiers Explained with Examples

## Introduction
Access modifiers control who can read or change the members of a class. They protect our data and make our intent clear to other developers. TypeScript offers `public`, `private`, `protected` and `readonly`. Note that TypeScript checks these rules at compile time only.

## The Four Modifiers
```ts
class BankAccount {
  public owner: string;
  private balance: number = 0;
  protected accountType: string = "Savings";
  readonly id: number;

  constructor(owner: string, id: number) {
    this.owner = owner;
    this.id = id;
  }

  deposit(amount: number): void {
    this.balance += amount;
  }
}

const account = new BankAccount("Rafi", 1);
account.owner = "Sara"; // OK
account.balance = 50;   // Error: private
account.id = 2;         // Error: readonly
```
The `public` modifier is the default, so anyone can access it. In the example, `owner` can be changed from outside. The `private` modifier limits access to the class itself, so `balance` changes only through `deposit`. A `protected` member is like private, but subclasses can use it too. Finally, `readonly` lets we set a value once, in the declaration or constructor, and never change it again. That is why `account.id = 2` is an error.

## Protected in a Subclass
```ts
class SavingsAccount extends BankAccount {
  describe(): string {
    return this.accountType;
  }
}
```
Here, `SavingsAccount` can read `accountType`, but outside code cannot.

## Conclusion
Use `private` to hide internal details. Use `protected` when subclasses need access. Use `readonly` for values that must never change. Because these rules disappear after compilation, they are not runtime security. Good habits with modifiers make classes safer and easier to understand.
