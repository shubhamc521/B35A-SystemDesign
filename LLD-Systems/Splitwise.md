# Splitwise LLD

Payment Management Application
- Application to manage payment done by multiple people in a group simplify them.
- Provide an ability to split the expense amoung users.

4 firends - 
Ram Shyam Nishant and Gargi.  ---> Went to ice cream parlour

Purchased cone.

Payment was done by RAM - 400

Ram Shyam Nishant Gargi
300 -100. -100    -100                                                   --- Equal Share

Went to Dmart and purchased different things.

                  Ram       Shyam       Nishant        Gargi
Cost of good      10         50          35             55    ==>  150
Paid by           150 
Net Amt           +140      -50          -35           -55               --- UnEqual Share [Exact] 

                  Ram       Shyam       Nishant       Gargi
                  60%       10%         20%           10%  
Paid By           400
Net               +160      -40         -80           -40                --- Percentage Share

A & B went to lunch.
A paid 600
B = -300

B needs to pay A 300 rs.    - [1st transaction]

C & B went on a dinner
B paid here 600
C = -300

C needs to pay 300rs to B    - [2nd Trasaction]

How we can minimize the trasactions? 

C can directly pay to A.  --- Everything will be settled in 1 transaction.




Problem: Design a payment tracking application that helps manage and track expences, both individualy and in group.

Requirements:

Functional:
    You went on a Goa trip.
    One Persona paid for hotel accomodation - 10,000

    In a dairy, Hotel Accomodation - Amount - Who all people are involved.

1. Expense Management
    - Add Expense : Users should be able to add the expense (10, 000 )
    - Edit Expense : Users can modify the expense
    - Delete Expense: Delete the expense
    - Settle Expense: Users can settle there expense to clear outstanding.

2. Group Management

    All the people going on a Goa trip will be added here.

    - Create Group 
    - Add/Edit/Settle expences.

3. Additional Features:

    - Comment: Users can add comment to expenses.
    - Activity Log: Track all events.
    - Authentication

Non Functional Requirement:
- Scalability
- Performance
- Data Consistency

Split Algorithms:

1. Equal Split
    - Friends splitting equal
    - Total Amount + Participant List [input]
    - Equal shares for all [output]

2. Exact Split
    - Unequal Share
    - Total Amount + Per - Person amount [input]
    - Custom amount per person

3. Percentage Split
    - Propotional Split 
    - Total Amount + Per - person percentage [input]
    - Custom Amount per person [output]



# Zero Sum Property:

SUM (all balances) = 0

Where:
    - Positive balance = Recieves money
    - Nagative Balance = Owes money

    Ram paid 400rs.

    Ram Shyam Nishant Gargi
    +300 -100 -100.   -100

    300 + (-100) + (-100) + (-100) = 0

    Addition of all pisitives and negatives  = 0

1. Equal Split Algorithm

Dinner Party:
- Total Bill = 900
- 3 friedns : Ram Nishant Gargi
- Ram paid the full amount
- Each person should pay 300

EQUAL_SPLIT(totalAmount, paidBy, Participants)
    1. numPeople = Length(participans)
    2. perPersonShare = TotalAmount / numPeople
    3. balances = {}

    4. For each Person in participants:
        IF person == paidBy:
        balances[person] = totalAmount - perPersonShare

        ELSE:
            balances[person] = -perPersonShare

    5. VERIFY: SUM(balnces.values) == 0
    6. return balances

2. EXACT SPLIT 

- Total 500
- Ram purchased 200rs
- Nishant Purchased 180rs
- Gargi Purchased 120rs

Nishant paid here 500

exactAmount = { RAM = 200,  Nishant = 180 , Gargi = 120 }

EXACT_SPLIT(totalAmount, paidBy, exactAmount):
    1. participants = key(exactAmount)

    2. sumOfShares = SUM (exactAmount.values())
    3. VARIFY: sumOfShares == TotalAmount
        Throw error if not equal

    4. balances {}

    5. FOR each person in participants:

        userShare = exactAmount[person]

        IF person == paidBy:
            balance = totalAmount - userShare
        
        ELSE:
            balances[Person] = -userShare
    
    6. VERIFY: SUM(balnces.values) == 0
    7. return balances

    
3. PERCENTAGE SPLIT

- Total = 2000
- DAD pays  50% (1000)
- Mom pays 30%. (600)
- You pays 20%  (400)

Dad paid total 2000.

percetanges = { DAD = 50%, MOM = 30%, YOU = 20% }

PERCENTAGE_SPLIT












# Data Model

User{
    userID uid,
    string ImageURL,
    int phonenumber,
    string bio,
    string email
}

Balance{
    string currency;
    int amount
}

Group{
    GroupID gid,
    List<User> users,
    string ImageURL,
    string tittle,
    string descripttion
}

// Expense - Individual or Group expenses, maps users to bal.
// Bilder design pattern will be used : Expense Builder.

Expense{
    expsenseID eid,
    bool isSettled,
    map<user, Balance> userbalance,
    GroupID gid,
    string tittle,
    int timestamp,
    string imageURL
}


// Strategy Design pattern should be used.
// Split Strategy

interface - SplitStrategy
EQUAL, EXACT and PERCENTAGE should implement this.

// Splitwise Class: Facade Pattern

Facade? To mange a;; the services without letting client know. Client will only talk with facade class.







