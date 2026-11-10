# How Generics Work in TypeScript and Why They Help with Promise<T>

## Introduction
Generics let you write one piece of code that works with many types while keeping type safety. Think of a generic as a labeled box: the label (the type) is filled in later.

## How Generics Work
```ts
function wrap<T>(value: T): T[] {
  return [value];
}

wrap(5);    // number[]
wrap("hi"); // string[]
```
`T` is a placeholder type. TypeScript infers it from the argument, so you reuse the function without falling back to `any`.

## Generics and Promise<T>
`Promise` is itself generic: `Promise<string>` means "a string, arriving later."
```ts
interface User {
  id: number;
  name: string;
}

async function fetchData<T>(url: string): Promise<T> {
  const response = await fetch(url);
  return response.json();
}

const user = await fetchData<User>("/api/user");
```
One function now serves every endpoint, and `user` is typed as `User`. Autocomplete works, and a typo like `user.nme` is caught at compile time.

## Conclusion
Generics give you reusable, type-safe code, and with `Promise<T>` they describe what async calls return. Remember that the type is a promise you make, so still validate data from untrusted APIs.
