# Chapter 2 Day 2 - Quest Submissions

#### 1. Explain why we wouldn't call changeGreeting in a script.

You wouldn't call changeGreeting inside of a script because, scripts are only used to view data not change it. Instead, you would call changeGreeting in a transaction. 

#### 2. What does the AuthAccount mean in the prepare phase of the transaction?

The AuthAccount type represents a signer's account, and it also accesses the data inside their account. This is done once, a transaction has been signed. 

#### 3. What is the difference between the prepare phase and the execute phase in the transaction?

The prepare phase in a transaction accesses the data in your account through the AuthAccount type; which represents the user's account. Whereas the execute phase can call functions in order to change data on the blockchain. Unlike the prepare phase, the execute phase cannot access a user's account data, through the AuthAccount type. 

#### 4. Add two new things inside your contract:
- A variable named myNumber that has type Int (set it to 0 when the contract is deployed)
- A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
![ch2-d2](/chapter2/images/ch2-d2.png)

- Add a script that reads myNumber from the contract

  ![ch2-d2-2](/chapter2/images/ch2-d2-2.png)


- Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. 

  ![ch2-d2-3](/chapter2/images/ch2-d2-3.png)
  
 - Verify that your number changed by running the script again.
  
    ![ch2-d2-4](/chapter2/images/ch2-d2-4.png)



