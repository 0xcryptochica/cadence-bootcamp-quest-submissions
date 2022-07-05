# Chapter 5 Day 3 - Quest Submissions

#### 1. What does "force casting" with as! do? Why is it useful in our Collection?
- Force casting will take a generic type and downcast it into a more specifc type. For example, in our _CryptoPoops_ contract we had to add a force cast to our _deposit_ function, in order to downcast the _@NonFungibleToken.NFT_ type to _@NFT_. This is useful in our Collection because, instead of being able to deposit any NFT into our collection, we can ensure that only the specific or correct NFTs are being deposited instead. 

#### 2. What does auth do? When do we use it?
- _Auth_ is used with references in order to downcast. Since, references need an authorized reference, we need to use _auth_ before the reference, in order to properly downcast it. For example, we used _auth_ in our CryptoPoops contract as well: 
  - _(&self.ownedNFTs[id] as auth &NonFungibleToken.NFT?)!_

#### 3. Take this contract, and add a function called borrowAuthNFT just like we did in the section called _"The Problem"_. Then, find a way to make it publically accessible to other people so they can read our NFT's metadata. Then, run a script to display the NFTs metadata for a certain id. 

```Cadence
import NonFungibleToken from 0x02
pub contract CryptoPoops: NonFungibleToken {
  pub var totalSupply: UInt64

  pub event ContractInitialized()
  pub event Withdraw(id: UInt64, from: Address?)
  pub event Deposit(id: UInt64, to: Address?)

  pub resource NFT: NonFungibleToken.INFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  // Make `borrowAuthNFT` public 
  pub resource interface CollectionPublic {
    pub fun borrowAuthNFT(id: UInt64): &NFT
  }

  pub resource Collection: NonFungibleToken.Provider, NonFungibleToken.Receiver, NonFungibleToken.CollectionPublic, CollectionPublic {
    pub var ownedNFTs: @{UInt64: NonFungibleToken.NFT}

    pub fun withdraw(withdrawID: UInt64): @NonFungibleToken.NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
            ?? panic("This NFT does not exist in this Collection.")
      emit Withdraw(id: nft.id, from: self.owner?.address)
      return <- nft
    }

    pub fun deposit(token: @NonFungibleToken.NFT) {
      let nft <- token as! @NFT
      emit Deposit(id: nft.id, to: self.owner?.address)
      self.ownedNFTs[nft.id] <-! nft
    }

    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    pub fun borrowNFT(id: UInt64): &NonFungibleToken.NFT {
      return (&self.ownedNFTs[id] as &NonFungibleToken.NFT?)!
    }

    pub fun borrowAuthNFT(id: UInt64): &NFT {
	    let ref = (&self.ownedNFTs[id] as auth &NonFungibleToken.NFT?)!
	    return ref as! &NFT
    }

    init() {
      self.ownedNFTs <- {}
    }

    destroy() {
      destroy self.ownedNFTs
    }

  }
  pub fun createEmptyCollection(): @NonFungibleToken.Collection {
    return <- create Collection()
  }

  pub resource Minter {

    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  init() {
    self.totalSupply = 0
    emit ContractInitialized()
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}
```
- Create Collection:

```Cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

transaction {
    prepare(signer: AuthAccount) {
        signer.save(<- CryptoPoops.createEmptyCollection(), to: /storage/CryptoPoopsCollection)
        signer.link<&CryptoPoops.Collection{NonFungibleToken.Provider, NonFungibleToken.Receiver, NonFungibleToken.CollectionPublic, CryptoPoops.CollectionPublic}>(/public/CryptoPoopsCollection, target: /storage/CryptoPoopsCollection)
    
    }

}
```
- Transaction used to mint NFTs:
```Cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

transaction(recipient: Address, name: String, favouriteFood: String, luckyNumber: Int) {
    prepare(signer: AuthAccount) {
        let minter = signer.borrow<&CryptoPoops.Minter>(from: /storage/Minter) ?? panic("This signer did not deploy this contract.")
        let recipientsCollection = getAccount(recipient).getCapability(/public/CryptoPoopsCollection).borrow<&CryptoPoops.Collection{NonFungibleToken.CollectionPublic}>() ?? panic("The recipient does not have a Collection.")

        let nft <- minter.createNFT(name: name, favouriteFood: favouriteFood, luckyNumber: luckyNumber)
        recipientsCollection.deposit(token: <- nft)
    }

}
```
- Script used to get IDs:
```Cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

pub fun main(address: Address): [UInt64] {
    let account = getAccount(address).getCapability(/public/CryptoPoopsCollection).borrow<&CryptoPoops.Collection{NonFungibleToken.CollectionPublic}>() ?? panic("This address does not have a Collection.")
    return account.getIDs()
}
```
- Script to read metadata:
```Cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

pub fun main(address: Address, id: UInt64): &CryptoPoops.NFT {
    let nftMetadata = getAccount(address).getCapability(/public/CryptoPoopsCollection).borrow<&CryptoPoops.Collection{CryptoPoops.CollectionPublic}>() ?? panic("Cannot access collection.")
    return nftMetadata.borrowAuthNFT(id: id)
}
```
