Here are the flowcharts in Markdown format:

**1) Multiply 2 numbers by taking input from the user**

```plaintext
### 1) Multiply 2 numbers by taking input from the user

**Flowchart:**
```plaintext
graph TD
A((Start))
A --> B(Input A)
B --> C(Input B)
C --> D(Multiply A by B and store the result in 'result')
D --> E(Output 'result')
E((End))
```

**Pseudocode:**
```plaintext
1. Start
2. Read A from the user
3. Read B from the user
4. Multiply A by B and store the result in 'result'
5. Display 'result'
6. End
```

**2) Perimeter of a triangle**

```plaintext
### 2) Perimeter of a triangle

**Flowchart:**
```plaintext
graph TD
A((Start))
A --> B(Input side1)
B --> C(Input side2)
C --> D(Input side3)
D --> E(Calculate the perimeter as 'perimeter = side1 + side2 + side3')
E --> F(Output 'perimeter')
F((End))
```

**Pseudocode:**
```plaintext
1. Start
2. Read side1 from the user
3. Read side2 from the user
4. Read side3 from the user
5. Calculate the perimeter as 'perimeter = side1 + side2 + side3'
6. Display 'perimeter'
7. End
```

**3) Find simple interest**

```plaintext
### 3) Find simple interest

**Flowchart:**
```plaintext
graph TD
A((Start))
A --> B(Input P)
B --> C(Input R)
C --> D(Input T)
D --> E(Calculate the simple interest as 'interest = (P * R * T) / 100')
E --> F(Output 'interest')
F((End))
```

**Pseudocode:**
```plaintext
1. Start
2. Read the principal amount 'P' from the user
3. Read the rate of interest 'R' from the user
4. Read the time period 'T' from the user
5. Calculate the simple interest as 'interest = (P * R * T) / 100'
6. Display 'interest'
7. End
```

**4) Print count of numbers from N to 1**

```plaintext
### 4) Print count of numbers from N to 1

**Flowchart:**
```plaintext
graph TD
A((Start))
A --> B(Input N)
B --> C(Set count = N)
C --> D{count > 0}
D -- Yes --> E(Output count)
E --> F(Decrement count by 1)
F --> D
D -- No --> G((End))
```

**Pseudocode:**
```plaintext
1. Start
2. Read N from the user
3. Set count = N
4. Repeat until count is greater than 0
   a. Output count
   b. Decrement count by 1
5. End
```

**5) Find factorial of a number**

```plaintext
### 5) Find factorial of a number

**Flowchart:**
```plaintext
graph TD
A((Start))
A --> B(Input N)
B --> C(Set factorial = 1)
C --> D{ i <= N}
D -- Yes --> E(Update factorial = factorial * i)
E --> F(Increment i by 1)
F --> D
D -- No --> G(Output factorial)
G((End))
```

**Pseudocode:**
```plaintext
1. Start
2. Read N from the user
3. Set factorial = 1
4. Repeat from i = 1 to N
   a. Update factorial = factorial * i
5. Display factorial
6. End
```

**6) Find whether a number is prime or not**

```plaintext
### 6) Find whether a number is prime or not

**Flowchart:**
```plaintext
graph TD
A((Start))
A --> B(Input N)
B --> C(Set isPrime variable to true)
C --> D{ i <= N-1 }
D -- Yes --> E{N % i == 0}
E -- Yes --> F(Set isPrime to false and break the loop)
F --> G(Increment i by 1)
G --> D
D -- No --> H{isPrime is true}
H -- Yes --> I(Output 'N is prime')
H -- No --> J(Output 'N is not prime')
I --> K((End))
J --> K
```

**Pseudocode:**
```plaintext
1. Start
2. Read N from the user
3. Set isPrime variable to true
4. Repeat from i = 2 to N-1
   a. If N is divisible by i, set isPrime to false and break the loop
5. If isPrime is true, then N is prime, else it's not prime
6. End
```
