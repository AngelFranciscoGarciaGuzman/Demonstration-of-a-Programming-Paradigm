# Demonstration-of-a-Programming-Paradigm
Evidence 4 of the course Implementation of Computational methods

# Demonstration of a Programming Paradigm

## 4th Evidence of the course “Implementation of Computational Methods”

### Context of the problem:

For this evidence, we will use a 1400 complexity problem from the website “Codeforces.com” called: B. Boot Camp

The problem is about planning the number of lectures to be conducted during the boot camp.

The boot camp will last for n days, and the BSU lecturers are planning to give some number of lectures during these days. Some days of the boot camp are already planned as excursion days, and no lectures should be held during these days. To make sure the participants don’t get too tired of learning to program, the number of lectures for each day should not exceed k1, and the number of lectures for each pair of consecutive days should not exceed k2.

The challenge is to calculate the maximum number of lectures that can be conducted during the boot camp. Formally, find the maximum integer m such that it is possible to choose n non-negative integers c1, c2, …, cn (where ci is the number of lectures held during day i) so that:

- The sum of all ci (c1+c2+⋯+cn) equals m.
- For each excursion day d, cd=0.
- For each day i, ci≤k1.
- For each pair of consecutive days (i,i+1), ci+ci+1≤k2.
  Note that there might be some non-excursion days without lectures (i.e., it is possible that ci=0 even if i is not an excursion day).

For our input, we will receive multiple lines of integers. 
The first line contains a single integer t (1≤t≤50) — the number of test cases. 

Each test case consists of two lines. 
The first line contains three integers n, k1, k2 (1≤n≤5000; 1≤k1≤k2≤200000). 
The second line contains one string s consisting of exactly n characters, each character is either 0 or 1. If si=0, then day i is an excursion day (so there should be no lectures during that day); if si=1, then day i is not an excursion day.

The output for each test case is one integer — the maximum possible value of m (the number of lectures that can be conducted).

So now that we have our problem, we will implement our model for further analysis.

### Model:

#### Implementation:

**Logic:** The solution utilizes dynamic programming to find the maximum number of lectures that can be conducted during the boot camp while adhering to the given constraints.

# Flow:

Initialize a 2D array dp to store the maximum number of lectures for each day considering the current day's lecture count and the previous day's lecture count.

Iterate through each day and for each day, iterate through possible lecture counts up to k1.

If it's an excursion day, update dp[i][0] by taking the maximum between the current maximum lecture count and the previous day's maximum lecture count.

If it's not an excursion day, iterate through possible lecture counts up to k1 for the previous day, and update dp[i][j] by taking the maximum between the current maximum lecture count and the sum of the lecture count for the previous day and the current day (if it doesn't exceed k2).

Finally, return the maximum lecture count from the last day.

Input: n (Number of days), k1 (Max lectures per day), k2 (Max lectures for consecutive days), days (Excursion days)

Initialize 2D array dp[n+1][k1+1]

         k1
     0  1  2  ... k1
   ___________________
 0 | 0  0  0  ... 0   | 
   |_________________|
 1 | -  -  -  ... -   | Day 1
   |_________________|
 2 | -  -  -  ... -   | Day 2
   |_________________|
 . |    ...           |
 . |_________________|
 . |    ...           |
   |_________________|
n-1| -  -  -  ... -   | Day n-1
   |_________________|
 n | -  -  -  ... -   | Day n
   |_________________|

Iterate through each day (i = 1 to n):
    If day i is an excursion day:
        Iterate through lecture counts for day i (j = 0 to k1):
            Update dp[i][0] by taking max(dp[i][0], dp[i-1][j])
    Else (day i is not an excursion day):
        Iterate through lecture counts for previous day (k = 0 to k1):
            Iterate through lecture counts for day i (j = 0 to k1):
                If sum of lectures for previous day and current day <= k2:
                    Update dp[i][j] by taking max(dp[i][j], dp[i-1][k] + j)

Return max value from last row of dp array as maximum possible lectures
This diagram illustrates how the dynamic programming approach works to find the maximum number of lectures that can be conducted during the boot camp while satisfying the given constraints.

## Implementation:

### Import Statements:
