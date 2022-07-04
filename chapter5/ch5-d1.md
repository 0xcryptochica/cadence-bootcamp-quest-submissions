# Chapter 5 Day 1 - Quest Submissions

#### 1. Describe what an event is, and why it might be useful to a client.
- An event is way of communicating that something has occurred within our smart contracts. This could be useful for a client because, if we had a _totalSupply_ variable in our contract (similar to the examples in the lesson), and used an event to update the _totalSupply_ when minting an NFT a client could see how many NFTs are still to be minted. 

#### 2. Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.
```Cadence
pub contract ArtistDiscography {

    pub event latestAlbum(id: UInt64, albumTitle: String, releaseDate: String)

    pub resource album {
        pub let id: UInt64
        pub var albumTitle: String
        pub var releaseDate: String
    

        init() {
            self.id = self.uuid
            self.albumTitle = "Call Me If You Get Lost"
            self.releaseDate = "June 25, 2021"

            emit latestAlbum(id: self.id, albumTitle: self.albumTitle, releaseDate: self.releaseDate)

        }
    }

    pub fun addNewAlbum(): @album {
        return <- create album()
    }

    init() {}

}

```

#### 3. Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.
```Cadence
pub contract ArtistDiscography {

    pub event newAlbum(id: UInt64, previousAlbum: String, albumTitle: String, numOfTracks: Int, numOfAlbums: Int)

    pub resource Album {
        pub let id: UInt64
        pub var previousAlbum: String
        pub var albumTitle: String
        pub var numOfTracks: Int
        pub var numOfAlbums: Int
    

    pub fun newAlbumTitle(albumTitle: String) {
        pre {
            albumTitle.length > 0: "Album title is too short."
        }
    }

    pub fun updateDiscography(numOfAlbums: Int) {
        post {
            self.numOfAlbums == before(self.numOfAlbums) + 1
        }
    }

    init() {
            self.id = self.uuid
            self.previousAlbum = "IGOR"
            self.albumTitle = "Call Me If You Get Lost"
            self.numOfTracks = 16 
            self.numOfAlbums = 5
            emit newAlbum(id: self.id, previousAlbum: self.previousAlbum, albumTitle: self.albumTitle, numOfTracks: self.numOfTracks, numOfAlbums: self.numOfAlbums)

        }

    }

    pub fun addNewAlbum(): @Album {
        return <- create Album()
    }

    init() {}

}
```

#### 4. For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions

- _func. numberOne()_: This function will log _'Jacob'_, because _name_ is equal to 5 characters in length. 

- _func. numberTwo()_: This function returns the value, _'Jacob Tucker'_ because it meets both the pre and post-conditions, and returns the concatenated value _result._

- _func. numberThree()_: _'self.number'_, will not log the updated number because, it does not meet the pre-condition and instead aborts the program.  

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
