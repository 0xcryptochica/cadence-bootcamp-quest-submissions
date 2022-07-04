# Chapter 5 Day 2 - Quest Submissions

#### 1. Explain why standards can be beneficial to the Flow ecosystem.
- Standards are beneficial because with standards it's easier to understand the type of contract you might be working with, and eliminating the need to implement a different functionality for each contract you wish to deploy. 

#### 2. What is YOUR favourite food?
- Fried chicken. 😋

#### 3. Please fix this code (Hint: There are two things wrong):

#### The contract interface:
```Cadence
pub contract interface ITest {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff {
    pub var favouriteActivity: String
  }
}
```

#### Within the implementing contract, we need to:
- Import _ITest_ & Add the _ITest_ contract interface.
- Remove the resource interface _Stuff_.
- Add the _ITest_ contract interface to the resource _Stuff_; _ITest.IStuff_

```Cadence
import ITest from 0x01 // Import ITest
pub contract Test: ITest { // Add the ITest contract interface
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    self.number = newNumber
    // self.number = 5
  }

  // We can remove the  
  // resource interface 'Stuff'
  
  pub resource Stuff: ITest.IStuff { // Add contract interface
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}
```
