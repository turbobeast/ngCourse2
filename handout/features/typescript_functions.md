# Typescript Functions

Defining function signatures is one of the main advantages of working with strongly typed languages.
As it allows you to document and enforce (at least at compile time) the contract between functions and their callers.

Adding types to a function is simple, individual parameter types are specified like any other variable definition and return types are defined after the function parentheses, before the function body.

```typescript
// a function that accepts a number and returns boolean
function oldEnough (age: number): boolean {
  return !!(age > 18)
}
```

## Optional Parameters

Explicitly defining every parameter can leave you with a function signature far stricter than what you need. Parameters can be made optional by adding a question mark to the end of the parameter name.

```typescript
function operation (cb?: Function): void {
  // do something
  const val = 'callback param'
  if (cb) {
    cb(val)
  }
}
```

## Generics

For polymorphic, reusable, functions, a type used within a function can be specified at call time with generics.

```javascript
// prepend the function parentheses with a generic type identifier in a set of <>
function doSomethingWithSet <T>(...args:Array<T>): T {
  args.forEach((arg) => {
    if (typeof arg === 'number') {
      // do something with number
    } else {
      // handle other type
    }
  })
  return args[0]
}

doSomethingWithSet<number>(53,2,5,2,42,65,2)
doSomethingWithSet<Object>({}, {}, {})
doSomethingWithSet<string>(1,2,3) // argument is not assignable to parameter of type string
```

## Class Constructor Functions

Typescript provides a shorthand for adding members to an instance. Prepend an access modifier (`public`, `private`, `protected`) to the parameter definition and the typescript compiler will take care of adding the member to your instance.  It will even enforce the behaviour specific your chosen access modifier (compile-time only).

```javascript
class Superhero {
  constructor (public name: string, private secretIdentity: string) {}
}

const batman = new Superhero('batman', 'bruce wayne')
batman.name // 'batman'
batman.secretIdentity // compiler error (but we, and the runtime javascript, know it's 'bruce wayne')
```