# Chapter 3 Day 5 - Quest Submissions

#### 1. For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.

Variable(s) / Function(s) | Read Scope(Area)  | Write Scope(Area) | Access Scope |
| ------------- | ------------- | ------------- | ------------- | 
| _pub(set) var a_  | 1, 2, 3, 4  | 1, 2, 3  | |
| _pub var b_  | 1, 2, 3, 4  | 1  | |
| _access(contract) var c_ | 1, 2, 3 | 1 | | 
| _access(self) var d_| 1 | 1 | |
| _pub fun publicFun_|  |  | 1, 2, 3, 4 |
| _access(contract) fun_|  |  | 1, 2, 3 |
| _access(self) fun_|  |  | 1 |
