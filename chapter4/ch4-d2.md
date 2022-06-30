# Chapter 4 Day 2 - Quest Submissions

#### 1. What does _.link()_ do?
- The _.link()_ function, links a resource to either the _/public/_ or _/private/_ paths. When you links something to either of these paths, you are then creating a capability. 

#### 2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.
-  By creating a capability we can use a resource interface to determine what data is publically available and accessible.  For example, if there was a specific function you wouldn't want to be publically accessible, you can use a resource interface and only expose or include which functions or variables you'd like to give access to. 

#### 3. Deploy a contract that contains a resource that implements a resource interface. Then, do the following:
- In a transaction, save the resource to storage and link it to the public with the restrictive interface.
- Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.
- Run the script and access something you CAN read from. Return it from the script.
