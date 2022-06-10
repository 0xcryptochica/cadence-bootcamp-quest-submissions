#### 1. Explain why we wouldn't call changeGreeting in a script.

You wouldn't call changeGreeting inside of a script because, scripts are only used to view data not change it. Instead, you would call changeGreeting in a transaction. 

#### 2. What does the AuthAccount mean in the prepare phase of the transaction?

The AuthAccount type accesses the data in a user's account, once a transaction is signed. 

#### 3. What is the difference between the prepare phase and the execute phase in the transaction?

The prepare phase in a transaction accesses the data in your account, whereas the execute phase can call functions in order to change data on the blockchain. Unlike the prepare phase, the execute phase cannot access a user's account data. 

#### 4. Add two new things inside your contract:
- A variable named myNumber that has type Int (set it to 0 when the contract is deployed)
- A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
![ch2-d2](https://user-images.githubusercontent.com/95149302/173110566-34624119-0c44-4c75-94fe-3d6b43d957b1.png)

- Add a script that reads myNumber from the contract

  ![ch2-d2-2](https://user-images.githubusercontent.com/95149302/173110829-f5347fb3-7034-44d3-ab18-b1a450674626.png)


- Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. 

  ![ch2-d2-3](https://user-images.githubusercontent.com/95149302/173110837-15321fe8-5065-4470-a270-440faabc2b24.png)
  
 - Verify that your number changed by running the script again.
  
    ![ch2-d2-4](https://user-images.githubusercontent.com/95149302/173111174-a35e0f81-3480-44f5-914b-5f26ceefe0c1.png)



