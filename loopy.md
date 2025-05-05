# Repetition: Loops and Recursion

Computers are good at repetition. That's part of why good software can save so much time. In programming, we have two main ways to do repetitive tasks.

1. **Loops** run code within a function multiple times.
2. **Recursion** is when a function calls itself to solve a smaller version of the same problem.

## Part 1: Loops

There are three important questions when it comes to a loop.
1. Where does it start?
2. When does it end?
3. How does it make progress towards termination?

There are two kinds of loops: `for` loops and `while` loops.

### Example 1: While loop
A while loop keeps going while a specific condition is true. 
```python
# Count to 3
n = 1          # Start with this value 
while n <= 3:   # Stop when the value gets too high
    print(n)
    n = n + 1   # Step towards the end by increasing the value
```

### Example 2: For loop
A for loop keeps going until it's run its code for every element in a sequence, like a list or a range of numbers. We generally use for loops when we know how many times we want to run a loop in advance.
```python
# Print list items
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```
Can you see how this loop makes progress towards termination?

### Example 3: Password, please
Let's try an example in the Python tutor. Remember, you'll need to call your function after you've defined it. 

```python
def check_password():
    tries = 3
    while tries > 0:
        guess = input("Enter password: ")
        if guess == "supersecurepassword123":
            print("Access granted")
            return
        tries = tries - 1
    print("Too many tries!")
```
Since we don't know how many times the user is going to guess the password, we don't use a for loop here. Instead, we use a while loop that runs until the user has tried too many times. 

### Example 4: Just for fun
Here's an example that might look familiar.
```python
for i in [3, 2, 1]:
    print(f"{i} little monkeys jumping on the bed")
    print("One fell off and bumped his head")
```

### Challenge
Change this while loop to a for loop:
```python
# Current while version
count = 5
while count > 0:
    print(count)
    count = count - 1
```

## Part 2: Recursion

A recursive function needs to cover two cases:
1. **Base case**: Solve the smallest/final version of the problem.
2. **Recursive case**: Call the function on a smaller version of the problem. 

**Example 1: Countdown**

Let's write a function that counts down from an input number. If we use a loop, that might look something like this:
```python
def countdown_loop(n):
    while n > 0:
        print(n)
        n = n - 1
    print("Go!")

countdown_loop(10)
```
Where does this loop start? When does it end? How does it make progress towards termination?

With a recursive function, we have two questions:
1. Does this problem contain a smaller problem?
2. What do I do with the smallest version of the problem?

To count down from 10, I could say `10` and then ask someone else to count down from 9. So if the problem is "how do I count down from n?" The smaller problem is "how do I count down from n - 1?"

What's the smallest version of this problem? If `n = 1`, I can say `1` and then ask someone else to count down from 0. But if `n = 0`, I shouldn't say `0` and ask someone to count down from -1. I should just stop counting. So this problem should never get smaller than `n = 0`. 

Let's write a function that solves this problem by saying `n` and then calling itself on `n - 1`, until it's time to stop counting. 

```python
def countdown(n):
    if n == 0:          # Base case
        print("Go!")
        return
    print(n)            # Step
    countdown(n - 1)    # Recursive case

countdown(10)
```
Not too different from the loop, right? Copy this code into the Python Tutor and click Visualize. Step through the function's execution. Notice how each recursive step adds a new stack frame. Then, once the base case is complete, each stack frame is removed in reverse. 

### Example 2

These days, most of us do our counting ourselves. Let's take a look at a recursion example where you actually have to pass the work to someone else.

Imagine you're sitting in a movie theater and want to know which row you're in, but it's so dark you can't see a label. All you can see is the row in front of yours, so you can't just count the rows either. How can you find out how many rows are in front of yours?

The smaller problem here is "how many rows are in front of the row before mine?" If you're in the front row, you know. A function to solve this recursively might look like this:

```python
def ask_seat_number(person):
    if person.is_first_row:          
        return 1
    return 1 + ask_seat_number(person.in_front)  

your_seat = ask_seat_number(you)
print("Your seat number is:", your_seat)
```
Each person asks the person in front of them. When they get an answer, they add 1 and pass it back up until it reaches you.

### Challenge

Make this recursive:
```python
def print_numbers(n):
    for i in range(1, n+1):
        print(i)
```

## When to use

It's better to use a loop when:
- You know exactly how many times you want to repeat an action
- You're working with a simple list
- Memory matters and you don't want too many stack frames

Recursion can be better when:
- Problems have natural smaller parts
- The recursive solution is easier to read
- You're dealing with nested information

## Best practices
1. Always check when your loops will stop.
2. Make sure your recursion has a base case.
3. Start with small test cases.
4. Practice!
