# Chapter 4 Day 3 - Quest Submissions

#### 1. Why did we add a Collection to this contract? List the two main reasons.
- To save time, because if we wanted to have a large supply of NFTs and saved all these at different storage paths, you'd have to remember each of these storage paths. Thus making the entire process very inefficient. 
- Only the account owner could store an NFT in their account storage, no else could mint an NFT. 

#### 2. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")

- In situations where you have _"nested resources,"_ you need to make sure you've declared a _destroy_ function, that'll manually destroy your nested resources. 

#### 3. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.
- Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.
  - Ideally it's not the greatest idea to let everyone mint their own NFT, this could cause security issues within our contract. For example, you would no longer have control over the total supply of the Collection. To resolve this issue we could create a resource where only the owner of the resource can mint an NFT. 

- Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?
  - This isn't good because, constantly having to remove data from our Collection isn't the most efficient way to read information about our NFTs. Instead we could create a resource interface that stores the metadata of each NFT, and then link this to the _/public/ path_. Allowing everyone to then be able to freely read information about our NFTs.
