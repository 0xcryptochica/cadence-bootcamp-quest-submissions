# Chapter 4 Day 4 - Quest Submissions

#### 1. Take our NFT contract so far and add comments to every single resource or function explaining what it's doing in your own words.
```Cadence
pub contract CryptoPoops {
  pub var totalSupply: UInt64

  // This is a resource named `NFT` that contains a name,
  // favourite food, and a lucky number
  pub resource NFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    // Here we're initializing our id, name, favourite food,
    // and lucky number
    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  // This resource interfaces exposes 3 different
  // functions, deposit(), getIDs(), and borrowNFT()
  pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT)
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
  }

  // This Collection resource lets us store 
  // multiple resources within the same storage path
  pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}

    // Deposits an NFT to our Collection
    pub fun deposit(token: @NFT) {
      self.ownedNFTs[token.id] <-! token
    }

    // Withdraws an NFT from our Collection
    pub fun withdraw(withdrawID: UInt64): @NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
              ?? panic("This NFT does not exist in this Collection.")
      return <- nft
    }

    // Returns an array of the NFT ids 
    // stored within our Collection
    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    // Returns references to the IDs
    // of the NFTs that are stored  
    // within our Collection
    pub fun borrowNFT(id: UInt64): &NFT {
      return (&self.ownedNFTs[id] as &NFT?)!
    }

    // Initializes our owned NFTs
    init() {
      self.ownedNFTs <- {}
    }

    // Destroys the ownedNFTs
    destroy() {
      destroy self.ownedNFTs
    }
  }

  // Creates a new empty Collection
  pub fun createEmptyCollection(): @Collection {
    return <- create Collection()
  }

  // The `Minter` resource allows only the contract
  // deployer to mint NFTs
  pub resource Minter {

    // Creates an NFT resource
    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    // Creates a `Minter` resource
    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  // Initializes our totalSupply and
  // saves the `Minter` resource to the account 
  // storage of the contract deployer
  init() {
    self.totalSupply = 0
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}

```
