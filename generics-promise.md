# How Generics Work in TypeScript and Why They Help with Promise<T>

## Introduction
Generics let we write one piece of code that works with many types while keeping type safety. Think of a generic as a labeled box whose label is filled in later. This matters a lot when we handle data that arrives asynchronously.

## How Generics Work
```ts
function wrap<T>(value: T): T[] {
  return [value];
}

wrap(5);    // number[]
wrap("hi"); // string[]
```
Here, `T` is a placeholder type. TypeScript infers it from the argument, so `wrap(5)` returns `number[]`. Without generics, we would have to use `any` and lose autocomplete and error checking. Generics give us reuse without giving up safety.

## Generics and Promise<T>
`Promise` is itself generic, so `Promise<string>` means "a string that arrives later."
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
This one function can serve every endpoint in our app. When we call it with `<User>`, the result is typed as `User`. Autocomplete now works on `user.name`. A typo like `user.nme` is caught at compile time instead of crashing at runtime.

## Conclusion
Generics make our code reusable and type-safe. With `Promise<T>`, they describe exactly what an async call returns. Remember that the type is only a promise we make, so we should still validate data from untrusted APIs. Start using them early and our async code will be much easier to maintain.
