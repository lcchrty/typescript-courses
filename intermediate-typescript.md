# intermediate typescript

## intro quiz - overview / review

**declaration merging** combines multiple declarations withyt e same name into a single definition

**unit type** a type that can only hold exactly one value
`infer` keyword purpose: extract a type aparameter our of another type within a conditional type's condition  

**top types** - can accept any value  

**mapped types** - transform types by creating new interfaces witht he same keys but different value types  

**variance** over type parameters --> the way types behave in relation to their type parameters -- includes: covariance, contravariance, bivariance, and invariance  

## declaration merging

* describes how various declarations stack on top of each other to form importable and exportable symbols
* alt: * when a single identifier (importable or exportable item with a name) has multiple things stacked on top of it such as a function, interface, and namespaces all sharing the same name

### identifiers

``` TypeScript
interface Fruit {
           
interface Fruit
  name: string
  mass: number
  color: string
}
 
const banana: Fruit = {
        
const banana: Fruit
  name: "banana",
  color: "yellow",
  mass: 183,
}

// both of these things are exportable
export { banana, Fruit }

```

* what if there were MULTIPLE declarations named Fruit?  
* what is an identifier?  
* why wouldn't i make a class called Fruit??  

**Identifiers Quiz**
how many distinct slots can an identifier have in TypeAscript thorugh declaration merging?  
*three: values, types, namespaces*  

How can you test whether an identifier has a value on it in TypeScript  
*Try to use it on the right-hand side of a variable assignment*  

What is unique about testing whether an identifier has a namespace in TypeScript?  
*There is no expression that will only work if something is a namespace; it must be verified by hovering over it*  

### namespaces

What's the point of `namespace`?  

* can be used as a type
* can't be used as a value
* jQuery example

### classes

* we benefit from declaration merging when we create classes
  * play on prototypal inheritance ??
* if you can assign it to a value it is *at least* a value

What two things does a TypeScript class declaration merge together?  
*A type for the instance and a value for the class constructor*

Why does TypeScript infer [1, 2, 3] as number[] instead of a specific tuple type?  
*Because arrays are mutable and TypeScript makes practical assumptions about their use*

What is the difference between TypeScript's readonly modifier and Object.freeze()?  
*readonly is a compile-time check that's stripped away, while Object.freeze() actually prevents runtime modifications*

How can you get TypeScript to infer more specific literal types for an object?  
*Use as const to make TypeScript infer as if it were a const declaration with readonly properties*

What is a simple test to determine if something is a value in TypeScript?  
*Try assigning it to a variable - if it works, there's at least a value present*

## top & bottom types

### top types

A top type (symbol: `⊤`) is a type that describes any possible value allowed by the system.

`any` allows typescript to play by regular javascript rules  
`unknown` typesx values cannot be used without applying a type guard

What is the key difference between the any type and the unknown type in TypeScript?  
*`unknown` requires type narrowing before use, while `any` disables type checking*

Why is the any type appropriate for console.log()?  
*Because it needs to accept and serialize any value that can be created in JavaScript*

What must you do before using a variable of type unknown in TypeScript?  
*You must use type guards to narrow down the type*
> covered type-guards in enterprise ts course @ [./packages/chat/src/type-guards.ts](./packages/chat/src/type-guards.ts)

What happens when you assign different types of values to a variable declared as any?  
*TypeScript allows all assignments without type checking*

### pratical uses of top types

``` JSON
// tsconfig.json
{
    // ...
    "useUnknownInCatchVariables": true,

    // 
}
```

* pay a price at runtime with type-guards
* unknown is good for API / schema errors
* an "opaque" value
* type-guards when talking to APIs that are NOT SaaS and won't know that it is changed -- makes errors easier to tracer

**Quiz**
What TypeScript compiler setting automatically types catch block variables as unknown?  
*UseUnknownInCatchVariables*

Why is it recommended to type catch block error variables as unknown instead of any?  
*It prevents assuming the error is a proper Error object before checking, since throwables could be strings or other objects*

When is it most appropriate to use typeguards for API responses?  
*When working with external APIs that you don't control and may change without notice*

What is an appropriate use case for the unknown type when passing values through code?  
*When treating a value as opaque that passes through library code and returns to the consumer unaltered*

What is the trade-off when using typeguards to validate API responses at runtime?  
*You pay a runtime cost but get more actionable errors when the API shape doesn't match expectations*

### objects & Empty Objects

almost top types - object & {}  
interfaces represent object types which is DIFFERENT than the type called object

null is not assignable to Empty Object

> what is the point of a non nullable?  

**QUIZ**  
What does the `object` type represent in TypeScript?  
*The set of all possible values except for primitives*  

Which of the following values are NOT accepted by the `object` type?  
*`number`, `string`, `boolean`, `null`, `undefined`, `symbol`, and `bigint`*

What is the empty `object` type `{}` allowed to accept?  
*All possible values except `null` and `undefined`*

How can you remove `null` and `undefined` from a union type like `string | number | null | undefined`?
*Use the `NonNullable` utility type or intersect with `{}`*

When strict `null` checks are disabled in tsconfig, how does `null` behave with the object type?  
*`null` is allowed as part of any type created*

### bottom types

if the types represent what will be at runtime - you should `never` get here

* I think I've handle every possible thing that could be
* exhaustive condition -- unreachable errors -- helpful for tracing in observalibilty tools/logging

### unit types
