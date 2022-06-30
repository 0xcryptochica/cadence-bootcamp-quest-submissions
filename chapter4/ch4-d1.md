# Chapter 4 Day 1 - Quest Submissions

#### 1. Explain what lives inside of an account.
- Inside an account lives contract code and account storage. Firstly, any contract that gets deployed to an account lives inside of that account; with multiple contracts being able to live inside of an account. Account storage, is all of your stored data, similar to a container of data that lives at a specific path. With there being three paths to access specific data _(/storage/, /public/, & /private/)_.  

#### 2. What is the difference between the _/storage/_, _/public/_, and _/private/_ paths?

- The main difference between the, _/storage/, /public/, and /private/_ paths is the data accessibility. The _/storage/_ path, is only accessible by the account owner and is where all of your data lives. Whereas the _/public/_ path is accessible to anybody. Opposite of the _/public/_ path is the _/private/_ path, in which can only be accessed by the account owner and select people the account owner gives access to. 
  - Although only an account owner can access their _/storage/_, they can also place things within both the _/public/_ and      _/private/_ paths. 

#### 3. What does _.save()_ do? What does _.load()_ do? What does _.borrow()_ do?

- The _.save()_ function, is used to write or save data to an account's storage. Meanwhile, the _.load()_ function takes data out of your account storage. Finally, the _.borrow()_ function can be used to reference data within an account, without having to remove the data from the account storage. 

#### 4. Explain why we couldn't save something to our account storage inside of a script.

- Scripts cannot alter or change data on the blockchain, therefore we can't save anything to our account storage inside of a script. 

#### 5. Explain why I couldn't save something to your account.

- You can't save anything to another user's account without them first signing a transaction, that contains the _AuthAccount_ type. 

#### 6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:
```Cadence
  pub contract ArtistDiscography {

    pub resource Discography {
        pub var artistName: String
        pub var numOfAlbums: Int

        init() {
            self.artistName = "Frank Ocean"
            self.numOfAlbums = 2
        }
    } 

    pub fun addNewArtist(): @Discography {
        return <- create Discography()
    }

}
```

- A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.
```Cadence


```

- A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
```Cadence


```
