---
layout: default
title: Swift - The Protocol Oriented Language
---
## Swift: The Protocol Oriented Language

I've been wanting to blog for some time now, but even though i've got ideas coming out of my ears it was still tough for me to figure out what the subject of my first post would be. Then I remembered an amazing WWDC video I watched a couple weeks back called "Protocol-Oriented Programming in Swift" by Dave Abrahams. This video struck a chord with me and hopefully the concepts i'll discuss can have an impact on the way you write code as well.

### The Big Picture
The phrase "Program to an 'interface', not an 'implementation'." was introduced in the famous Gang of Four Book "Design Patterns: Elements of Reusable Object-Oriented Software" in 1995. It's a well known methodology to experienced OOP software engineers, but from my experiences and those of others that I've spoken with it seems to be overlooked in most undergraduate computer science programs. Think about how much more time you spent discussing how "Dog inherits from Animal but that doesn't mean Animal is a Dog", than the usefulness of interfaces. At their core swift protocols are interfaces (with some extra sprinkles). I'm hoping that as Swift grows in popularity among young developers this abstraction pattern will grow with it. 

### The Problem with Inheritance
While inheritance is super powerful I think it's important that we don't overuse it. In Dave Abrahams' talk he describes some of the main issues with inheritance in Swift: 
- You can only inherit from one superclass
- Having one superclass can lead to bloat in that class
- That superclass has to be chosen at the time of your subclass definition
- You must have an understanding of the superclass so that you don't break its invariants

Luckily Swift has an alternative to dealing with these issues...Protocols.

### The Protocol
For those unfamiliar with a protocol heres a simple example of how to define one.

```
protocol Tasty {
  func numberOfIngredients() -> Int
}
```
Then you could implement it like this.

```
stuct Cupcakes : Tasty{
  let ingredients = ["flour", "sugar", "butter", "milk", "eggs"]
  
  func numberOfIngredients() -> Int{
    return ingredients.count
  }
}
```
Thats a very simple example of protocols but I think it says a lot about some of the advantages of protocols. First of all, notice that I used a struct to define the cupcakes rather than a class. Structs are value types in swift which means that on assignment its value is copied rather than referenced. This is an important point because allows us to feel confident that our instances will not be mutated somewhere else in the code, a problem that can lead to some nasty bugs. 

Another great thing that protocols do is allow for a type to conform to multiple other types. Let's look at a similar example:

```
stuct Beer : Tasty, Drinkable{
  let ingredients = ["water", "oats", "barley", "sugar", "alcohol"]
  let waterWeightFluidOZ : Double = 21.0
  let alcoholWeightFluidOZ : Double = 1.0
  
  func numberOfIngredients() -> Int{
    return ingredients.count
  }
  
  func sizeInFluidOZ() -> Double {
    return waterWeightFluidOZ + alcoholWeightFluidOZ //I know it's way oversimplified
  }
  
}
```
Then you could define Drinkable like this:

```
protocol Drinkable {
  func sizeInFluidOZ() -> Double
}
```
Conforming to multiple types is a great tool for categorizing the specific traits of an object. While both cupcakes and beer are Tasty cupcakes certainly are not drinkable.

Rather than trying to fit all of this conformance into one superclass or creating a tree of abstraction which must already exist before our class definition, protocols allow us to create objects of multiple types which can be added or modified at anytime with relative ease.

### Protocol Extensions

Extensions are not new to Swift developers, in Swift 1.0 you could easily extend classes to add functionality to them. Swift 2.0 introduced Protocol Extensions, which are nothing short of amazing. Let's add a requirement to our Tasty protocol called belongsToFoodGroup which returns an enum of FoodGroup. 
 
```
protocol Tasty {
  func numberOfIngredients() -> Int
  func belongsToFoodGroup() -> FoodGroup
}

``` 
For the extension we'll add both the belongsToFoodGroup() function which was specified in our protocol and a caloricLevel() function which was not.

```
extension Tasty {
  func belongsToFoodGroup() -> FoodGroup {
    return Foodgroup.Confections
  }
  
  func caloricLevel() -> CaloricLevel {
    return CaloricLevel.High
  }
}
```

Here we've implemented two extension functions, each of which adds some default behavior to the Tasty protocol. Let's see what happens when we implement and call these methods. 

```
extension TastyGrains : Tasty {
  func belongsToFoodGroup() -> FoodGroup {
    return FoodGroup.Grains
  }
  
  func caloricLevel() -> CaloricLevel {
    return CaloricLevel.Medium
  }
}

let treat = TastyGrains()
treat.belongsToFoodGroup() //Foodgroup.Grains
treat.caloricLevel() //CaloricLevel.Medium
```
That basically works exactly as you would think it should, the belongsToFoodGroup() method returns .Grains, and the CaloricLevel returns .Medium. How about if we make some slight changes though.

```
let treat : Tasty = TastyGrains()
treat.belongsToFoodGroup() //Foodgroup.Grains
treat.caloricLevel() //CaloricLevel.High
```
What you'll notice is that the belongsToFoodGroup() is still customized by the TastyGrains extension, however the caloricLevel defaults back to the Tasty extension value. The difference in these two functions is that belongsToFoodGroup() is backed by a requirement which allows for customization at that point. 

Now let's get into the fun stuff.

Protocol extensions also can be conditional. Let's add an isFluid() method to the original extension of tasty.

```
extension Tasty {
    func isFluid() -> Bool {
        return false
    }
}

```
Let's add another extension which is conditional and see what happens.

```
extension Tasty where Self : Drinkable {
    func isFluid() -> Bool {
        return true
    }
}

let tasyBeer = Beer()
tastyBeer.isFluid() //true

let tastyCupcake = Cupcake()
tastyCupcake.isFluid() //false
```
Wow look at that! The Tasty protocol extension was able to correctly identify that beer is a fluid without ever specifying that in any of the beer methods. 

The whole concept of protocol extensions gives protocols much of the functionality and extensibility that can only be found through class inheritance in Swift 1.0. My favorite thing about this new feature which was discussed in the WWDC talk by Dave Abrahams is how it can enhance your testing. Protocols lead to decoupled code, and don't hold any of the underlying implementation details of their objects. This kind of decoupling makes them great for creating mock's to make your awesome tests even better. This is a pretty broad subject and i'm sure your getting bored by now so i'm not going to cover it in this post but hopefully i'll be writing a post dedicated to this use case in the near future.

### Conclusion

Protocols are awesome abstractions, and with extensions we now can truly rely on them to operate as types of their own. They allow us to do more modeling with structs, improving upon the overall immutability of our code. Even though protocols have become so feature rich, classes still do have their place as pointed out by Dave Abrahams. Typically this is when either the framework requires you use class types or when you want implicit sharing among your instances. 

Protocols are easily one of my favorite things about the language, and I can't wait to start using extensions in my own code. I hope you enjoyed the post, i'll try to make the next one a bit shorter.