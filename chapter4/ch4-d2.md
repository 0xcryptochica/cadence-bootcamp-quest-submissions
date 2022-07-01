# Chapter 4 Day 2 - Quest Submissions

#### 1. What does _.link()_ do?
- The _.link()_ function, links a resource to either the _/public/_ or _/private/_ paths. When you links something to either of these paths, you are then creating a capability. 

#### 2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.
-  By creating a capability we can use a resource interface to determine what data is publically available and accessible.  For example, if there was a specific function you wouldn't want to be publically accessible, you can use a resource interface and only expose or include which functions or variables you'd like to give access to. 

#### 3. Deploy a contract that contains a resource that implements a resource interface. 
```Cadence
pub contract ArtistDiscography {
 
    pub resource interface IDiscography {
        pub var artistName: String
        pub var numOfAlbums: Int
    }

    pub resource Discography: IDiscography {
        pub var artistName: String
        pub var numOfAlbums: Int
        pub var firstAlbum: String
        pub var mostRecentAlbum: String

        pub fun addNewDiscography(newArtistName: String, newNumOfAlbums: Int, newFirstAlbum: String, newMostRecentAlbum: String): String {
            self.artistName = newArtistName
            self.numOfAlbums = newNumOfAlbums
            self.firstAlbum = newFirstAlbum
            self.mostRecentAlbum = newMostRecentAlbum

            return self.artistName
        }

        init() {
            self.artistName = "Frank Ocean"
            self.numOfAlbums = 2
            self.firstAlbum = "Channel Orange"
            self.mostRecentAlbum = "Blonde"
        }
    } 

    pub fun addNewArtist(): @Discography {
        return <- create Discography()
    }

    init() {}

}
```

#### Then, do the following:
- In a transaction, save the resource to storage and link it to the public with the restrictive interface.
```Cadence
import ArtistDiscography from 0x01

transaction() {
    prepare(signer: AuthAccount) {
        signer.save(<- ArtistDiscography.addNewArtist(), to: /storage/MyArtistDiscography)
        signer.link<&ArtistDiscography.Discography>(/public/MyArtistDiscography, target: /storage/MyArtistDiscography)
    
    }

    execute {}
}

```

- Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.
```Cadence
import ArtistDiscography from 0x01
pub fun main(address: Address): String {
    let artistCapability: Capability<&ArtistDiscography.Discography{ArtistDiscography.IDiscography}> = 
      getAccount(address).getCapability<&ArtistDiscography.Discography{ArtistDiscography.IDiscography}>(/public/MyArtistDiscography)
    
    let discographyResource: &ArtistDiscography.Discography{ArtistDiscography.IDiscography} = artistCapability.borrow() ?? panic("The capability does not exist.")

    return discographyResource.firstAlbum // Produces an error: `member of restricted type does not accessible: firstAlbum`
}

```

- Run the script and access something you CAN read from. Return it from the script.
```Cadence
import ArtistDiscography from 0x01
pub fun main(address: Address): String {
    let artistCapability: Capability<&ArtistDiscography.Discography{ArtistDiscography.IDiscography}> = 
      getAccount(address).getCapability<&ArtistDiscography.Discography{ArtistDiscography.IDiscography}>(/public/MyArtistDiscography)
    
    let discographyResource: &ArtistDiscography.Discography{ArtistDiscography.IDiscography} = artistCapability.borrow() ?? panic("The capability does not exist.")

    return discographyResource.artistName
}

```
