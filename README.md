Sure, I can help you create the flowcharts and pseudocode for each of the given questions. Below is the Markdown file with the questions, pseudocode, and flowcharts:

### Question 1: Multiply 2 numbers by taking input from the user

**Pseudocode:**
```
1. Input firstNumber
2. Input secondNumber
3. Set result = firstNumber * secondNumber
4. Display result
```

**Flowchart:**
```
start -> Input firstNumber -> Input secondNumber -> 
         firstNumber * secondNumber -> Display result -> end
```

### Question 2: Perimeter of a triangle

**Pseudocode:**
```
1. Input side1
2. Input side2
3. Input side3
4. Set perimeter = side1 + side2 + side3
5. Display perimeter
```

**Flowchart:**
```
start -> Input side1 -> Input side2 -> Input side3 ->
         side1 + side2 + side3 -> Display perimeter -> end
```

### Question 3: Find simple interest

**Pseudocode:**
```
1. Input principal
2. Input rate
3. Input time
4. Set interest = (principal * rate * time) / 100
5. Display interest
```

**Flowchart:**
```
start -> Input principal -> Input rate -> Input time ->
         (principal * rate * time) / 100 -> Display interest -> end
```

### Question 4: Print count of numbers from N to 1

**Pseudocode:**
```
1. Input N
2. Initialize count = N
3. Repeat while count >= 1
    a. Display count
    b. Set count = count - 1
4. End loop
```

**Flowchart:**
```
start -> Input N -> count = N -> 
         repeat -> Display count -> count = count - 1 -> 
         until count >= 1 -> end loop -> end
```

### Question 5: Find the factorial of a number

**Pseudocode:**
```
1. Input number
2. Set factorial = 1
3. Repeat while number > 1
    a. Set factorial = factorial * number
    b. Set number = number - 1
4. End loop
5. Display factorial
```

**Flowchart:**
```
start -> Input number -> factorial = 1 -> 
         repeat -> factorial = factorial * number -> 
         number = number - 1 -> until number > 1 -> 
         Display factorial -> end loop -> end
```

### Question 6: Find whether a number is prime or not

**Pseudocode:**
```
1. Input number
2. Set isPrime = true
3. Repeat for i from 2 to number - 1
    a. If number is divisible by i, set isPrime = false and break loop
4. End loop
5. If isPrime is true, display "Number is prime"
   Else, display "Number is not prime"
```

**Flowchart:**
```
start -> Input number -> isPrime = true -> 
         repeat for i from 2 to number - 1 -> 
         if number % i == 0 -> isPrime = false -> break loop -> 
         Display result -> end loop -> end
```

### Question 7: Check if a valid triangle or not

**Pseudocode:**
```
1. Input side1
2. Input side2
3. Input side3
4. If (side1 + side2 > side3) and (side1 + side3 > side2) and (side2 + side3 > side1)
    a. Display "Valid Triangle"
   Else
    b. Display "Not a Valid Triangle"
```

**Flowchart:**
```
start -> Input side1 -> Input side2 -> Input side3 ->
         If (side1 + side2 > side3) and (side1 + side3 > side2) and (side2 + side3 > side1) ->
         Display "Valid Triangle" -> else -> Display "Not a Valid Triangle" -> end
```

### Question 8: Print 1 to N but only even numbers

**Pseudocode:**
```
1. Input N
2. Initialize number = 1
3. Repeat while number <= N
    a. If number is even, display number
    b. Set number = number + 1
4. End loop
```

**Flowchart:**
```
start -> Input N -> number = 1 -> 
         repeat -> if number is even -> Display number -> 
         number = number + 1 -> until number <= N -> 
         end loop -> end
```

### Question 9: Find the maximum of three numbers

**Pseudocode:**
```
1. Input number1
2. Input number2
3. Input number3
4. Set maxNumber = number1
5. If number2 > maxNumber, set maxNumber = number2
6. If number3 > maxNumber, set maxNumber = number3
7. Display maxNumber
```

**Flowchart:**
```
start -> Input number1 -> Input number2 -> Input number3 -> 
         maxNumber = number1 -> 
         If number2 > maxNumber -> maxNumber = number2 -> 
         If number3 > maxNumber -> maxNumber = number3 -> 
         Display maxNumber -> end
```
