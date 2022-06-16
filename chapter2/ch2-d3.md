#### 1. In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.
```JavaScript
pub fun main() {

    var favPeople: [String] = ["Arya Stark", "Tyrion Lannister", "Sandor Clegane"]
    log(favPeople)

}

```

#### 2. In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!
```JavaScript
pub fun main() {

    var socialMedia: {String: UInt64} = {"YouTube": 1, "Twitter": 2, "Instagram": 3, "Reddit": 4, "LinkedIn": 5, "Facebook": 0}

}
```

#### 3. Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).

The force unwrap operator _!_, returns the values within an optional. If there is a value inside of the optional, _!_, will return it. However if there is a nil value, the program will panic and abort execution. 
 
```JavaScript
pub fun main(): UInt64 {
    var favPeople: {String: UInt64} = {"Arya Stark": 1, "Tyrion Lannister": 2, "Sandor Clegane" : 3}
    return(favPeople["Arya Stark"])
}

```
In this example, we get an error similar to the question below _(mismatched types. expected UInt64, got UInt64?)_, to fix this we can use the force unwrap operator _!_.

```JavaScript

pub fun main(): UInt64 {
    var favPeople: {String: UInt64} = {"Arya Stark": 1, "Tyrion Lannister": 2, "Sandor Clegane" : 3}
    return(favPeople["Arya Stark"])!
}
```

#### 4. Using this picture below, explain...
- What the error message means
- Why we're getting this error
- How to fix it

![wrongcode](/chapter2/images/wrongcode.png)

In the provided code, we get an error because the returned type is an optional, and the returned value does not match this. Since the type is an optional, String? must be used rather than just String; As it results in an error. To fix this, we can instead use the force unwrap operator _!_. 

```JavaScript
pub fun main(): String {

    let thing: {Address: String} = {0x01: "One", 0x02: "Two", 0x03: "Three"}
    return(thing[0x03]!)

}
```

