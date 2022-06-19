# Chapter 3 Day 1 - Quest Submissions

#### 1. In words, list 3 reasons why structs are different from resources.

Structs and resources at first glance may seem similar, however they are very different. Mainly due to the fact that, Structs can be copied, lost or overwritten, and can also be created anywhere. This is howeverm false for resources. 

#### 2. Describe a situation where a resource might be better to use than a struct.

A situation in which a resource is better to use than a struct is when creating an NFT. Since resources are difficult to lose and impossible to copy, they are an extremely secure way to store data.  

#### 3. What is the keyword to make a new resource?

The keyword to make a new resource is _create._

#### 4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

A resource cannot be created inside of a script or transaction, and can only be created inside of a contract. 

#### 5. What is the type of the resource below?
```Cadence
pub resource Jacob {

}
```
The type of this resource is _Jacob._

#### 6. Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.
```Cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // there is 1 here // Added @ in front of the resource type. 
        let myJacob <- create Jacob() // there are 2 here // Added <- and Create. 
        return <- myJacob // there is 1 here // Added <-
    }
}
```


