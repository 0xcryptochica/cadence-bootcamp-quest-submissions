# Chapter 5 Day 1 - Quest Submissions

#### 1. Describe what an event is, and why it might be useful to a client.
- An event is way of communicating that something has occurred within our smart contracts. This could be useful for a client because, if we had a _totalSupply_ variable in our contract (similar to the examples in the lesson), and used an event to update the _totalSupply_ when minting an NFT a client could see how many NFTs are still to be minted. 

#### 2. Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.
```Cadence


```

#### 3. Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.
```Cadence


```

#### 4. For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.
```Cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }

}
```
