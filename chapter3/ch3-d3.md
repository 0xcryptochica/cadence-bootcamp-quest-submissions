# Chapter 3 Day 3 - Quest Submissions

#### 1. Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.
``` Cadence
pub contract HorrorFilms {

    pub var dictionaryOfFilms: @{String: Film}

    pub resource Film {
        pub let filmName: String
        pub let releaseDate: Int
        pub let director: String
        pub let runtime: String

        init(_filmName: String, _releaseDate: Int, _director: String, _runtime: String ) {
            self.filmName = _filmName
            self.releaseDate = _releaseDate
            self.director = _director
            self.runtime = _runtime
        }

    }


    pub fun getFilm(key: String): &Film? {
        return &self.dictionaryOfFilms[key] as &Film?
    }

    init() {
        self.dictionaryOfFilms <- {
            "Friday the 13th": <- create Film(_filmName: "Friday the 13th", _releaseDate: 1980, _director: "Sean S. Cunningham", _runtime: "1h 35min"),
            "Nightmare On Elm Street": <- create Film(_filmName: "Nightmare On Elm Street", _releaseDate: 1984, _director: "Wes Craven", _runtime: "1hr 31min"),
            "Scream": <- create Film(_filmName: "Scream", _releaseDate: 1996, _director: "Wes Craven", _runtime: "1hr 51min")
        }
    }

}
```

#### 2. Create a script that reads information from that resource using the reference from the function you defined in part 1.
```Cadence
import HorrorFilms from 0x01

pub fun main(): String {
  let resourceRef = HorrorFilms.getFilm(key: "Friday the 13th")
  return resourceRef.filmName

}
```

Returns, ```Cadence {"type":"String","value":"Friday the 13th"}```

#### 3. Explain, in your own words, why references can be useful in Cadence.

- References are useful in Cadence because they can be used to interact with data without even having to have that specific piece of data. You can also interact with resources through references, thus eliminating the need to move the resource. 
