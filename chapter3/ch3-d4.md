# Chapter 3 Day 4 - Quest Submissions

#### 1. Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)
Two things resource interfaces can be used for are, specifying a certain set of requirements that can be implemented. As well as determining what information within a resource you want to allow access or expose to select/certain people. 

#### 2. Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.

```Cadence
pub contract ArtistDiscography {

    pub resource interface IDiscography {
        pub var artistName: String
        pub var numOfAlbums: Int
    }

    pub resource Discography {
        pub var artistName: String
        pub var numOfAlbums: Int

        pub fun addNewArtist(newArtistName: String): String {
            self.artistName = newArtistName
            return self.artistName
        } 

    init () {
        self.artistName = "Frank Ocean"
        self.numOfAlbums = 2
    }
    }

    pub fun noInterface() {
        let newArtistName: @Discography <- create Discography() 
        newArtistName.addNewArtist(newArtistName: "Tyler the Creator")
        log(newArtistName.addNewArtist)

        destroy newArtistName
    }

    pub fun yesInterface() {
        let newArtistName: @Discography{IDiscography} <- create Discography()
        newArtistName.addNewArtist(newArtistName: "Tyler the Creator")

        log(newArtistName.artistNam)

        destroy newArtistName
    }

}

```

#### 3. How would we fix this code? 
```Cadence 
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```
To fix this code, we need to:
- Add a 'changeGreeting' function to our struct interface
- Add the 'favouriteFruit' variable to the struct, 'Test'.
- Initialize the 'favouriteFruit' variable with your favourite fruit. ;)

```Cadence 
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String // Add a 'changeGreeting' func. 
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String // Add the 'favouriteFruit' var.

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Bananas" // Initialize the favouriteFruit var.
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```
