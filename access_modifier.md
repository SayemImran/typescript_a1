# TypeScript Access Modifiers Explained with Examples

## Introduction
Access modifiers control who can read or change the members of a class. They protect your data and make your intent clear. TypeScript checks them at compile time only.

## The Four Modifiers
```ts
class BankAccount {
  public owner: string;
  private balance: number;
  protected accountType: string = "Savings";
  readonly id: number;

  constructor(owner: string, balance: number, id: number) {
    this.owner = owner;
    this.balance = balance;
    this.id = id;
  }

  deposit(amount: number): void {
    this.balance += amount;
  }
}

const account = new BankAccount("Rafi", 100, 1);
account.owner = "Sara"; // OK
account.balance = 0;    // Error: private
account.id = 2;         // Error: readonly
```
- `public` is the default and works anywhere.
- `private` works only inside the class, so `balance` changes only through `deposit`.
- `protected` is like private, but subclasses can use it too.
- `readonly` can be set once, in the constructor, and never changed.

```ts
class SavingsAccount extends BankAccount {
  describe(): string {
    return this.accountType; // OK
  }
}
```

## Conclusion
Use `private` to hide internals, `protected` to share with subclasses, and `readonly` for values that must not change. These rules disappear after compilation, so they are not runtime security.
