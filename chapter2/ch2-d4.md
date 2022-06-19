# Chapter 2 Day 4 - Quest Submissions

#### 1. Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile).
```Cadence
pub contract clubInformation {

    pub struct clubHistory {
        pub let clubName: String
        pub let clubAbbrv: String
        pub let championshipsWon: Int
        pub let stadium: String
        pub let founded: Int

        init(_clubName: String, _clubAbbrv: String, _championshipsWon: Int, _stadium: String, _founded: Int) {
            self.clubName = _clubName
            self.clubAbbrv = _clubAbbrv
            self.championshipsWon = _championshipsWon
            self.stadium = _stadium
            self.founded = _founded
        }
    }

    init() {}

}
```


#### 2. Create a dictionary or array that contains the Struct you defined.
```Cadence
pub contract clubInformation {

    pub var clubs: {Address: clubHistory}

    pub struct clubHistory {
        pub let clubName: String
        pub let clubAbbrv: String
        pub let championshipsWon: Int
        pub let stadium: String
        pub let founded: Int

        init(_clubName: String, _clubAbbrv: String, _championshipsWon: Int, _stadium: String, _founded: Int) {
            self.clubName = _clubName
            self.clubAbbrv = _clubAbbrv
            self.championshipsWon = _championshipsWon
            self.stadium = _stadium
            self.founded = _founded
        }
    }

    init() {
      self.clubs = {}
    }

}
```


#### 3. Create a function to add to that array/dictionary.
```Cadence
pub contract clubInformation {

    pub var clubs: {Address: clubHistory}

    pub struct clubHistory {
        pub let clubName: String
        pub let clubAbbrv: String
        pub let championshipsWon: Int
        pub let stadium: String
        pub let founded: Int

        init(_clubName: String, _clubAbbrv: String, _championshipsWon: Int, _stadium: String, _founded: Int) {
            self.clubName = _clubName
            self.clubAbbrv = _clubAbbrv
            self.championshipsWon = _championshipsWon
            self.stadium = _stadium
            self.founded = _founded
        }
    }
    
    pub fun addClub(clubName: String, clubAbbrv: String, championshipsWon: Int, stadium: String, founded: Int, account: Address) {
        let newClub = clubHistory(_clubName: clubName, _clubAbbrv: clubAbbrv, _championshipsWon: championshipsWon, _stadium: stadium, _founded: founded, _account: account)
        self.clubs[account] = newClub
    }

    init() {
      self.clubs = {}
    }

}


```


#### 4.Add a transaction to call that function in step 3.
```Cadence
import clubInformation from 0x01

transaction(clubName: String, clubAbbrv: String, championshipsWon: Int, stadium: String, founded: Int, account: Address) {

    prepare(signer: AuthAccount) {}

    execute {
        clubInformation.addClub(clubName: clubName, clubAbbrv: clubAbbrv, championshipsWon: championshipsWon, stadium: stadium, founded: founded, account: account)
        log("Club Added.")
    }

}
```


#### 5.Add a script to read the Struct you defined.
```Cadence
import clubInformation from 0x01

pub fun main(account: Address): clubInformation.clubHistory? {
    return clubInformation.clubs[account]
}
```

