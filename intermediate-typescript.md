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

Identifiers Quiz
how many distinct slots can an identifier have in TypeAscript thorugh declaration merging?
three: values, types, namespaces

How can you test whether an identifier has a value on it in TypeScript
Try to use it on the right-hand side of a variable assignment
