# Chapter 3 Day 2 - Quest Submissions

#### 1. Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them.
```Cadence
pub contract championsLeague {
    pub var arrayOfClubs: @[Clubs]
    pub var dictionaryOfClubs: @{String: Clubs}

    pub resource Clubs {
        pub let clubAcronym: String
        init() {
            self.clubAcronym = "PSG"
        }
    }

    // Adding & Removing From The Array
   
    pub fun addClubToArray(clubs: @Clubs) {
        self.arrayOfClubs.append(<- clubs)
    }


    pub fun removeClubFromArray(index: Int): @Clubs {
        return <- self.arrayOfClubs.remove(at: index)
    }

    // Adding & Removing From The Dictionary
    
    //Using <-!
    pub fun addClubToDictionary(clubs: @Clubs) {
        let key = clubs.clubAcronym
        self.dictionaryOfClubs[key] <-! clubs
    }

    // Using the double move syntax
    pub fun addClubToDict(clubs: @Clubs) {
        let key = clubs.clubAcronym

        let oldClubs <- self.dictionaryOfClubs[key] <- clubs
        destroy oldClubs
    }

    pub fun removeClubFromDict(key: String): @Clubs {
        let clubs <- self.dictionaryOfClubs.remove(key:key)!
        return <- clubs 
    }

    init() {
    self.arrayOfClubs <- []
    self.dictionaryOfClubs <- {}
    }

}
```
