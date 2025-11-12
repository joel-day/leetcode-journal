# LeetCode Workspace

**Welcome to my custom mono-repo for practicing LeetCode, which doubles as a journal for my solutions.**

- The repo includes a custom flashcard UI and bash scripts.

- To setup for yourself, see the 'Workspace Set-up' section at the bottom of this ReadMe. 


# My Solutions

![Solution Image](data/raw/sol.jpg)

Photo by <a href="https://unsplash.com/@olav_ahrens?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Olav Ahrens Røtne</a> on <a href="https://unsplash.com/photos/person-playing-magic-cube-4Ennrbj1svk?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>

- For each solution, I provide the Intuition, Approach, and Code in Python and Javascript. Source: 'Top Interview 150' list on LeetCode.

- I try to go beyond just finding a solution that works and instead find one that is optimized to minimize both time and space complexity. For example, avoiding nested loops with n^2 time complexity, and creating new variables only when necessary. 

- I prioritize understanding the logic over memorization of specific functions. Instead of using LLM models like ChatGPT to help work through problems, I use them only to find isolated code or functions that can get me through each logical step of a problem. 

- I am stronger with python, so after initially solving the problem with python, I then convert it to JavaScript.
## ＃120 -  Is Subsequence💥
### Input/Output
```python
# Input
s = "abc"
t = "ahbgdc"

# Output
true
```

#### Intuition:
To see if the substring is in the string, Loop through each string. At each stage advance to the next value on the string but only advance to the next char in the substring if it matches the value in the string. If you get to the end of the substring before the end of the string return true. 

#### Approach:
- Loop through the strings until you pass the last index of either one. 
- Iterate through the values of the main string. At each iteration move to the next value in the main string.
- only add one to i if it matches the value in the main string.
- return true if i == len(s) means each letter was found in the string in order. 

#### Code:
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i = 0
        j = 0

        while i < len(s) and j < len(t):
            if s[i] == t[j]:
                i+=1
            j+=1
        return i == len(s)
```
```javascript
var isSubsequence = function(s, t) {
        let i = 0;
        let j = 0;

        while (i < s.length && j < t.length) {
            if (s[i] === t[j]) {
                i++;
            }
            j++;
        }

        return i === s.length;
};
```
## ＃121 - Valid Palindrome💥
### Input/Output
```python
# Input
s = "A man, a plan, a canal: Panama"

# Output
True
```

#### Intuition:
The goal here is to see if the string is a valid palendrome after removing non letters. To do this first clean the list and then test to see if it equals iself in reverse.

#### Approach:
- loop through the string joining only characters that are are alphanumeric
- check if the cleaned list is equal to itself in reverse

#### Code:
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        cleaned = ''.join(char for char in s if char.isalnum()).lower()
        if cleaned == cleaned[::-1]:
            return True
        else:
            return False
```
```javascript
var isPalindrome = function(s) {
            const cleaned = s.split('').filter(char => /[a-zA-Z0-9]/.test(char)).join('').toLowerCase();
        return cleaned === cleaned.split('').reverse().join('');
};
```
## ＃122 - Merge Sorted Array 💥
### Input/Output
```python
# Input
nums1 = [1,2,3,0,0,0]
m = 3
nums2 = [2,5,6]
n = 3

# Output
[1,2,2,3,5,6]
```

#### Intuition:
The goal here is to combine two lists both sorted in asc order into one sorted list. The challenge is to do it in place. So, iterate across the last values of each str from the end and add the larger of the two to the end of the first string. The key here is that the first list will have placeholders at the end to accommodate for the extra letter in the second string. Make sure to start at the end to be able to do it in place. 

#### Approach:
- create variables for each of the index (m, n, and m +n)
- loop over values in the n list from the back and test if it’s greater than the same index in the m list.
- add the higher value to the end of the original list
- subtract one from the index variable associated with the str with the larger value
- repeat


#### Code:
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        midx = m - 1
        nidx = n - 1 
        right = m + n - 1

        while nidx >= 0:
            if midx >= 0 and nums1[midx] > nums2[nidx]:
                nums1[right] = nums1[midx]
                midx -= 1
            else:
                nums1[right] = nums2[nidx]
                nidx -= 1

            right -= 1
```
```javascript
var merge = function(nums1, m, nums2, n) {
    let midx = m - 1;
    let nidx = n - 1;
    let right = m + n - 1;

    while (nidx >= 0) {
        if (midx >= 0 && nums1[midx] > nums2[nidx]) {
            nums1[right] = nums1[midx];
            midx--;
        } else {
            nums1[right] = nums2[nidx];
            nidx--;
        }
        right--;
    } 
};
```
## ＃123 - Remove Element 💥
### Input/Output
```python
# Input
nums = [3,2,2,3]
val = 3

# Output
[2,2]
```

#### Intuition:
The goal here is to remove all instances of a value in a string in place. To do this first count how many times that value appears, then remove that value from the list that many times. Once removed calculate the length using len(). 

#### Approach:
- Count the amount of times the value to remove appears
- for each of these times, remove that value from the list. 
- then return the length of that list after removal

#### Code:
```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        for i in range(nums.count(val)):
            nums.remove(val)
        return len(nums)
```
```javascript
var removeElement = function(nums, val) {
    while (nums.includes(val)) {
        nums.splice(nums.indexOf(val), 1);
    }
    return nums.length;
};
```
## ＃124 - Remove Duplicates from Sorted Array 💥
### Input/Output
```python
# Input
nums = [1,1,2]


# Output
[1,2]
```

#### Intuition:
The goal here is to remove the duplicates from an array in place and return the length without duplicates

#### Approach:
- Create a variable to track the amount of non-duplicates
- loop through each value (skipping the first) and if it equals the value before do nothing and moves on. If it is different, then add it to the k's position and add 1 to k. 


#### Code:
```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0

        k = 1 
        for i in range(1, len(nums)):
            if nums[i] != nums[i-1]:
                nums[k] = nums[i]
                k+=1
        return k
```
```javascript
function removeDuplicates(nums) {
    if (nums.length === 0) {
        return 0;
    }

    let k = 1;
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] !== nums[i - 1]) {
            nums[k] = nums[i];
            k++;
        }
    }

    return k;
}
```
## ＃125 - Remove Duplicates from Sorted Array II 💥
### Input/Output
```python
# Input
nums = [1,1,1,2,2,3]

# Output
[1,1,2,2,3]
```

#### Intuition:
The goal here is to remove the values from a list in place such that no value appears more than two times. 

#### Approach:
- First create a current variable to track the number of values kept and a current value which will handle the more than twice logic
- Then loop through each word, if it doesn’t equal the one before, change the value where index = current. Then add one to the current.
- If it is the same as the one before, add 1 to count, and only if count is 1 or less add the value where index = current.

#### Code:
```python
class Solution:
    def removeDuplicates(self, nums):
        count = 0
        current = 1
        for i in range(1, len(nums)):
            if nums[i] != nums[i - 1]:
                count = 0
                nums[current] = nums[i]
                current += 1
            else:
                count += 1
                if count <= 1:
                    nums[current] = nums[i]
                    current += 1
        return current
```
```javascript
var removeDuplicates = function(nums) {
    let count = 0;
    let current = 1;

    for (let i = 1; i < nums.length; i++) {
        if (nums[i] !== nums[i - 1]) {
            count = 0;
            nums[current] = nums[i];
            current++;
        } else {
            count++;
            if (count <= 1) {
                nums[current] = nums[i];
                current++;
            }
        }
    }

    return current;
};
```
## ＃126 - Majority Element 💥
### Input/Output
```python
# Input
nums = [3,2,3]

# Output
3
```

#### Intuition:
The goal here is to find the majority element. There is guaranteed to be a majority element where over half the values are that element. The trick is assigning the first value as the majority, adding one whenever you see it and subtracting it when you don’t. When the count hits zero, reassign the majority element to that value. This works because there always is a value appearing more than half the time. 

#### Approach:
- Traverse through the list
- If count is 0 and majority candidate is different from current element, update the majority candidate and set count to 1
- If the current element is the same as the majority candidate, increase the count
- If the current element is different from the majority candidate, decrement the count


#### Code:
```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        count = 0
        majority = 0

        # Traverse through the list
        for i in range(len(nums)):
            if count == 0 and majority != nums[i]:
                # If count is 0 and majority candidate is different from current element,
                # update the majority candidate and set count to 1
                majority = nums[i]
                count += 1
            elif majority == nums[i]:
                # If current element is the same as the majority candidate,
                # increment the count
                count += 1
            else:
                # If current element is different from the majority candidate,
                # decrement the count
                count -= 1

        return majority
```
```javascript
var majorityElement = function(nums) {

    let count = 0;
    let majority = 0;

    for (let i = 0; i < nums.length; i++) {
        if (count === 0 && majority !== nums[i]) {
            majority = nums[i];
            count += 1;
        } else if (majority === nums[i]) {
            count += 1;
        } else {
            count -= 1;
        }
    }

    return majority;

};
```
## ＃127 - Rotate Array 💥
### Input/Output
```python
# Input
nums = [1,2,3,4,5,6,7]
k = 3

# Output
[5,6,7,1,2,3,4]
```

#### Intuition:
The goal here is to rotate (shift) the values down x indexes. To solve this use slice assignment. First take the x values to shift off of the back of the list and put them on the front. One small hurdle is you can replace first few list values beofre you move them. So creating a temp list is required. 

#### Approach:
- find the remaider of k and n. 
- create a temp list holding the last k values in the list. 
- move the first len(nums) - k values forward k spaces. 
- change the first k values of the list to the temp strign values

#### Code:
```python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k = k % n
        if k == 0: return

        temp = nums[-k:]
        nums[k:] = nums[:-k]
        nums[:k] = temp 
```
```javascript
var rotate = function(nums, k) {

    const n = nums.length;
    k = k % n;
    if (k === 0) return;

    const temp = nums.slice(-k);         // Copy the last k elements
    for (let i = n - 1; i >= k; i--) {
        nums[i] = nums[i - k];           // Shift elements right by k
    }
    for (let i = 0; i < k; i++) {
        nums[i] = temp[i];               // Insert rotated elements
    }

};
```
## ＃128 - Best Time to Buy and Sell Stock 💥
### Input/Output
```python
# Input
prices = [7,1,5,3,6,4]

# Output
5
```

#### Intuition:
Find the most amount you could have buying and selling one stock one time over a given period. To do this loop through keeping track of the lowest price so far, at each step subtract the days price from the lowest so far to see the profit. return the max of these values. 

#### Approach:
- create a min_price variable staring at index 0. 
- loop through each following days price 
- subtract the days price from the min_price, if this is larger any before, set is as max_profit
- update the min_price using min

#### Code:
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        min_price = prices[0]
        max_profit = 0
        
        for price in prices[1:]:
            max_profit = max(max_profit, price - min_price)
            min_price = min(min_price, price)
            
        return max_profit
```
```javascript
var maxProfit = function(prices) {

    if (prices.length === 0) return 0;

    let minPrice = prices[0];
    let maxProfit = 0;

    for (let i = 1; i < prices.length; i++) {
        maxProfit = Math.max(maxProfit, prices[i] - minPrice);
        minPrice = Math.min(minPrice, prices[i]);
    }

    return maxProfit;

};
```
## ＃129 - Best Time to Buy and Sell Stock II 💥
### Input/Output
```python
# Input
prices = [7,1,5,3,6,4]

# Output
7
```

#### Intuition:
Find the most profit you can make on one stock where you can only hold one stock at a time. youcan sell and buy on the same day. find the max profit. 

#### Approach:
- loop through each day. 
- if you are arnt holding a stock and the price is going up - buy
- if you are holding stock and the price is going down - sell
- last bit of code to sell the last stock. 

#### Code:
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        holding_stock = 0
        stock_value = 0 
        profit = 0

        for i in range(0, len(prices) - 1):
            print(i, prices[i])

        


            if holding_stock == 0:

                if prices[i] < prices[i+1]:

                    holding_stock = 1

                    stock_value = prices[i]

            else:

                
                if prices[i+1]  < prices[i]:

                    profit += prices[i] - stock_value

                    stock_value = 0

                    holding_stock = 0


            print(holding_stock, stock_value, profit)

        if holding_stock == 1:

            profit += prices[-1] - stock_value

            stock_value = 0

            holding_stock = 0


        return profit
```
```javascript
var maxProfit = function(prices) {

    let holdingStock = false;
    let stockValue = 0;
    let profit = 0;

    for (let i = 0; i < prices.length - 1; i++) {
        // console.log(i, prices[i]); // Optional debug

        if (!holdingStock) {
            if (prices[i] < prices[i + 1]) {
                holdingStock = true;
                stockValue = prices[i];
            }
        } else {
            if (prices[i + 1] < prices[i]) {
                profit += prices[i] - stockValue;
                holdingStock = false;
                stockValue = 0;
            }
        }
    }

    if (holdingStock) {
        profit += prices[prices.length - 1] - stockValue;
    }

    return profit;
};
```
## ＃130 - Jump Game 💥
### Input/Output
```python
# Input
nums = [2,3,1,1,4]

# Output
true
```

#### Intuition:
The goal is to see if you could reach the end of the list if you can only jump as many times as the value at that position. To do this, at each stage keep track of the farthest you can go (using max of the current value and current max) and if this value equals the total distance - its possible. 

#### Approach:
- return true is list is empty and flase if the first value is 0.
- initiate max distance variable
- Loop through each number and find the max of itself and the current max_dstance variable
- this is the idstance and if this is 0 return false, if it is greater than the totoal length o flist return true. 
- otherwise subtract one from the max_distance and final_distance (payment to take a step, and one less to go)
- repeat

#### Code:
```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        possibility = False
        final_distance = len(nums) - 1

        if final_distance < 1:
            return True

        if nums[0] == 0:
            return False

        max_distance = 0

        for i in range(0,len(nums)-1):
            distance = max(max_distance, nums[i])

            if distance == 0:
                return False

            if distance >= final_distance:
                return True

            max_distance = distance - 1

            final_distance -= 1
```
```javascript
var canJump = function(nums) {

    let possibility = false;
    let finalDistance = nums.length - 1;

    if (finalDistance < 1) {
        return true;
    }

    if (nums[0] === 0) {
        return false;
    }

    let maxDistance = 0;

    for (let i = 0; i < nums.length - 1; i++) {
        let distance = Math.max(maxDistance, nums[i]);

        if (distance === 0) {
            return false;
        }

        if (distance >= finalDistance) {
            return true;
        }

        maxDistance = distance - 1;
        finalDistance -= 1;
    }

    return false;
};
```

## ＃131 - Jump Game II 💥
### Input/Output
```python
# Input
nums = [2,3,1,1,4]

# Output
2
```

#### Intuition:


#### Approach:
- create max_distance and current_end variables
- loop through each number
- max_distance = max(max_distance, i + nums[i]) - add i because at each iteration it is one position closer to end. 
- at each step update the max_distance and check if at the current end
- if so add a jump and update current_end to = max_distance
- repeat

#### Code:
```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        jumps = 0
        current_end = 0
        max_distance = 0

        for i in range(0, len(nums)-1):
            max_distance = max(max_distance, i + nums[i])

            if i == current_end:
                jumps += 1
                current_end = max_distance

        return jumps
```
```javascript
function jump(nums) {
    let jumps = 0;
    let currentEnd = 0;
    let maxDistance = 0;

    for (let i = 0; i < nums.length - 1; i++) {
        maxDistance = Math.max(maxDistance, i + nums[i]);

        if (i === currentEnd) {
            jumps++;
            currentEnd = maxDistance;
        }
    }
    return jumps;
}

```
## ＃132 - H-Index 💥
### Input/Output
```python
# Input
citations = [3,0,6,1,5]

# Output
3
```
#### Intuition:
The goal here is to find the h index for a researcher, where h is the at least h papers that have been published at least 8 times. So, for each paper, count how many other papers have <= the amount in the current one, and if this is greater than the value of the current item, then set h to max(current_h, current_value)

#### Approach:
- loop over each paper
- loop over each paper and count the amount of other paper have <= the amount of this one
- if it is larger than the value itself, set h to the max of the current h and this current value

#### Code:
```python
class Solution(object):
    def hIndex(self, citations):
        """
        :type citations: List[int]
        :rtype: int
        """
        h = 0
        count = 0


        for current_item in citations:


            for item in citations:
                if item >= current_item:
                    count += 1

            if count >= current_item:
                h = max(current_item, h)

            elif count != 0:
                h = max(count, h)


            count = 0

        return h
```
```javascript
var hIndex = function(citations) {
    let h = 0;
    let count = 0;

    for (let currentItem of citations) {
        for (let item of citations) {
            if (item >= currentItem) {
                count += 1;
            }
        }

        if (count >= currentItem) {
            h = Math.max(currentItem, h);
        } else if (count !== 0) {
            h = Math.max(count, h);
        }

        count = 0;
    }

    return h;
};
```
## ＃133 - Insert Delete GetRandom O(1) 💥
### Input/Output
```python
# Input
["RandomizedSet","insert","remove","insert","getRandom","remove","insert","getRandom"]
[[],[1],[2],[2],[],[1],[2],[]]

# Output
[null,true,false,true,1,true,false,2]
```

#### Intuition:
The goal is to implement a class that can add remove and display a random number from a list. The class initiates a value_to_index dictionary and a values list. Using these variables allows me to shift the value to remove to the end of the list and use pop to remove as opposed to iterating and shifting the list. The dictionary and list will not always stay in the same order. 

#### Approach:
- initiate a value_to_index dictionary and a values list.
- if the command is to insert add it to the list and dict and return true if it is not in the list. return false if it is.
- for del - if it is not present return false, otherwise it finds its location via the index in the dict and then swap it with the value at the end. then remove it using pop for the list and del for the index. 
- return random element from list

#### Code:
```python
import random

class RandomizedSet:
    def __init__(self):
        self.val_to_index = {}  # Dictionary to store value -> index mapping
        self.values = []  # List to store values

    def insert(self, val):  # Removed type hints
        if val in self.val_to_index:
            return False  # Value already exists, so don't insert
        
        self.values.append(val)  # Add value to list
        self.val_to_index[val] = len(self.values) - 1  # Store index in dictionary
        return True

    def remove(self, val):  # Removed type hints
        if val not in self.val_to_index:
            return False  # Value not in set, so can't remove
        
        # Get index of element to remove
        index_to_remove = self.val_to_index[val]
        last_element = self.values[-1]  # Get last element in the list

        # Swap the last element with the one to remove
        self.values[index_to_remove] = last_element
        self.val_to_index[last_element] = index_to_remove

        # Remove last element
        self.values.pop()
        del self.val_to_index[val]

        return True

    def getRandom(self):  # Removed type hints
        return random.choice(self.values)  # Get random element from list
```
```javascript
class RandomizedSet {
    constructor() {
        this.list = [];
        this.map = new Map();
    }

    search(val) {
        return this.map.has(val);
    }

    insert(val) {
        if (this.search(val)) return false;

        this.list.push(val);
        this.map.set(val, this.list.length - 1);
        return true;
    }

    remove(val) {
        if (!this.search(val)) return false;

        const index = this.map.get(val);
        this.list[index] = this.list[this.list.length - 1];
        this.map.set(this.list[index], index);
        this.list.pop();
        this.map.delete(val);
        return true;
    }

    getRandom() {
        const randomIndex = Math.floor(Math.random() * this.list.length);
        return this.list[randomIndex];
    }
}

```
## ＃134 - Product of Array Except Self 💥
### Input/Output
```python
# Input
nums = [1,2,3,4]

# Output
[24,12,8,6]
```

#### Intuition:
The goal here is to return a list where each element is the product of all the all the other values besides itself. To do this in place, a product variable is created = to all the values multiplied. For each output values instead of multiplying the others together, just divide the product variable by the values. The last problem to overcome is the 0s. If more than 1 all values are 0, if 1 zero, the index with the 0 will be the only non-zero output value. 

#### Approach:
- count zeros and calculate the total product of all variables
- if more than 1 zero return a list of all 0s. 
- if exactly one zero returns a list of nearly all 0's, just the location of the 0 will be the product of all the others. 
- (after taking care of 0 instances) return a list where each value is the product/ value. 

#### Code:
```python
class Solution:
    def productExceptSelf(self, nums):
        product = 1
        zeroCount = 0
        n = len(nums)
        result = [0] * n

        # Step 1: Calculate product of all non-zero elements and count zeros
        for num in nums:
            if num == 0:
                zeroCount += 1
            else:
                product *= num

        # Step 2: Handle the cases based on zero count
        if zeroCount > 1:
            return result  # More than one zero, all elements will be zero
        if zeroCount == 1:
            # If there's exactly one zero, the product of all other elements is placed in that position
            for i in range(n):
                if nums[i] == 0:
                    result[i] = product
        else:
            # If there are no zeros, divide the total product by each element
            for i in range(n):
                result[i] = product // nums[i]

        return result
        
```
```javascript
var productExceptSelf = function(nums) {
    const n = nums.length;
    const answer = new Array(n).fill(1);

    let left = 1;
    for (let i = 0; i < n; i++) {
        answer[i] = left;
        left *= nums[i];
    }

    let right = 1;
    for (let i = n - 1; i >= 0; i--) {
        answer[i] *= right;
        right *= nums[i];
    }

    return answer;
};
```
## ＃135 - Gas Station 💥
### Input/Output
```python
# Input
gas = [1,2,3,4,5]
cost = [3,4,5,1,2]

# Output
3
```
#### Intuition:
The goal here is to see if it is possible to travel through the list given the cost to move (cost) and the energy you get (gas). To move to the next city there needs to be more gas than costs. If there is less gas than the cost across the whole list return -1. Otherwise, it is possible, just find the string index. To do this, loop through the index at each starting point. calculate the gas at each step, if it ever ends under 0, move to the next possible starting point. There is only one solution (provided). 

#### Approach:
- check if total gas > cost. If not return 0 - it is not possible.
- Next create a start variable (output) and a current gas variable
- to find the starting index, loop through each starting point and at each step, calculate the current gas(gas-cost)
- if it ever ends a step < 0, exit. The starting index will never go under 0


#### Code:
```python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        if sum(gas) < sum(cost):
            return -1

        start = 0
        currentGas = 0

        for i in range(len(gas)):
            currentGas += (gas[i] - cost[i])
            if currentGas < 0:
                currentGas = 0
                start = i + 1
        return start
```
```javascript
class Solution {
    canCompleteCircuit(gas, cost) {
        let total_tank = 0, curr_tank = 0, start_index = 0;
        for (let i = 0; i < gas.length; i++) {
            total_tank += gas[i] - cost[i];
            curr_tank += gas[i] - cost[i];
            if (curr_tank < 0) {
                start_index = i + 1;
                curr_tank = 0;
            }
        }
        return total_tank >= 0 ? start_index : -1;
    }
}
```
## ＃136 - Candy 💥
### Input/Output
```python
# Input
ratings = [1,0,2]

# Output
5
```

#### Intuition:
The goal here is to distribute candies to kids. Where each kid gets at least one but kids with a higher rating than their neighbors should get more. To do this first give one candy to each kid. Then from left to right, if the kid has more candy than the kid to their left, give them one more candy than the neighboring kid. Then go from right to left. Doing the same, giving one more candy than the kid but this time return the max of the current value and 1 + the neighboring value. 

#### Approach:
- create an output list with all 1s
- loop from left to right adding 1 + the left neighbor if the value is greater.
- loop from right to left, update the output list to max(current value, 1 + right neighbor) if the kid has a higher value. 
- return the sum 

#### Code:
```python
class Solution:
    def candy(self, ratings):
        n = len(ratings)
        candies = [1] * n
        
        for i in range(1, n):
            if ratings[i] > ratings[i - 1]:
                candies[i] = candies[i - 1] + 1
        
        for i in range(n - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candies[i] = max(candies[i], candies[i + 1] + 1)
        
        return sum(candies)
```
```javascript
/**
 * @param {number[]} ratings
 * @return {number}
 */
var candy = function(ratings) {
    const n = ratings.length;
    let totalCandies = n;
    let i = 1;

    while (i < n) {
        if (ratings[i] === ratings[i - 1]) {
            i++;
            continue;
        }

        let currentPeak = 0;
        while (i < n && ratings[i] > ratings[i - 1]) {
            currentPeak++;
            totalCandies += currentPeak;
            i++;
        }

        if (i === n) {
            return totalCandies;
        }

        let currentValley = 0;
        while (i < n && ratings[i] < ratings[i - 1]) {
            currentValley++;
            totalCandies += currentValley;
            i++;
        }

        totalCandies -= Math.min(currentPeak, currentValley);
    }

    return totalCandies;    
};
```
## ＃137 - Trapping Rain Water 💥
### Input/Output
```python
# Input
height = [0,1,0,2,1,0,1,3,2,1,2,1]

# Output
6
```
#### Intuition:
The goal is to calculate the amount of water that would settle if the list values were an elevation map. meaning [2, 1, 2] would create a small bowl when graphed. Calculate the total water it can trap if it rains. To this first go from left to right, at each point, if it is not the new highest point, add the difference between itself and the current max. This will capture all the water between the starting point and the maximum point. To calculate the water trapped after the max point, do the same thing from right to the max point. 

#### Approach:
- loop through the list. 
- if the value is <= the current max, add the difference between the max height and the value to the water count,
- if the value is >= the current max adds the water count to results, set it to zero and update the max
- then loop from right to the max index, doing the same thing but in reverse


#### Code:
```python
class Solution(object):

    def trap(self, height):
        n = len(height)
        
        result = 0
        maxI, waterBlock = 0,0
        for i in range(1,n):
            if height[i] >= height[maxI]:
                result += waterBlock
                waterBlock = 0
                maxI = i
            waterBlock += (height[maxI] - height[i])

        end = maxI - 1
        maxI, waterBlock = n-1,0
        for i in range(n-2,end,-1):
            if height[i] >= height[maxI]:
                result += waterBlock
                waterBlock = 0
                maxI = i
            waterBlock += (height[maxI] - height[i])

        return result
```
```javascript
var trap = function(height) {
        let i = 0;
        let left_max = height[0];
        let sum = 0;
        let j = height.length - 1;
        let right_max = height[j];
        while (i < j) {
            if (left_max <= right_max) {
                sum += left_max - height[i];
                i++;
                left_max = Math.max(left_max, height[i]);
            } else {
                sum += right_max - height[j];
                j--;
                right_max = Math.max(right_max, height[j]);
            }
        }
        return sum;
    }
```
## ＃138 - Roman to Integer 💥
### Input/Output
```python
# Input
s = "III"

# Output
3
```

#### Intuition:
The goal here is to convert roman numerals to integers. It can be done by iterating through each numeral, adding its value to a variable if is greater than the next numeral and subtracting from the variable if it is smaller. 

#### Approach:
- create a dictionary mapping each roman numeral to its value
- loop through each numeral, if it isn’t the last, and has a value smaller than the next numeral subtract it from the result variable
- otherwise add its value to the variable

#### Code:
```python
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        rom_to_int = {
            'I': 1, 'V':5, 'X':10, 'L':50,
            'C':100, 'D':500, 'M':1000}

        result = 0

        for i in range(len(s)):
            if i + 1 < len(s) and rom_to_int[s[i]] < rom_to_int[s[i + 1]]:
                result -= rom_to_int[s[i]]
            else:
                result += rom_to_int[s[i]]
        return result
```
```javascript
var romanToInt = function(s) {
    let res = 0;
    const roman = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    };

    for (let i = 0; i < s.length - 1; i++) {
        if (roman[s[i]] < roman[s[i + 1]]) {
            res -= roman[s[i]];
        } else {
            res += roman[s[i]];
        }
    }

    return res + roman[s[s.length - 1]];    
};
```
## ＃139 - Game of Life 💥
#### Input/Output
```python
# Input
board = [[0,1,0],[0,0,1],[1,1,1],[0,0,0]]

# Output
output = [[0,0,0],[1,0,1],[0,1,1],[0,1,0]]
```

#### Intuition:
The goal is to apply the game of life to this board - in-place. This is solved in two steps. 1. Update each value to a temporary label based on its neighbors. 2. Map the labels to the final 0/1 values. To solve the inplace problem, when iterating across values, instead of counting all values of 1 in the neighbors count all values with an absolute value of 1. If a value needs to be changed from 1 to 0, first mark it as -1, For values that were dead and now alive use 2. so they fail the == 1 check when looking for currently alive neighbors. Once everthing is labeled, convert values >= 1 to 1 and values < 1 to 0. 

#### Approach:
- Iterate over each matrix value
- count the amount of live neighbors
- Apply the approiate label (-1, 2) or keep the existing value. 
- Once each value has been labeled map (-1, 2) to (0, 1)

#### Code:
```python
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        directions = [(1,0),(1,-1),(0,-1),(-1,-1),(-1,0),(-1,1),(0,1),(1,1)]
        for i in range(len(board)):
            for j in range(len(board[0])):
                live=0
                for x,y in directions: 
                    if (i+x<len(board) and i+x>=0) and (j+y<len(board[0]) and j+y>=0) and abs(board[i+x][j+y])==1:
                        live+=1
                if board[i][j]==1 and (live<2 or live>3):    
                    board[i][j]=-1
                if board[i][j]==0 and live==3:                  
                    board[i][j]=2
        for i in range(len(board)):
            for j in range(len(board[0])):
                board[i][j]=1 if(board[i][j]>0) else 0
        return board
```
```javascript
var gameOfLife = function(board) {
    const directions = [
        [1, 0], [1, -1], [0, -1], [-1, -1],
        [-1, 0], [-1, 1], [0, 1], [1, 1]
    ];

    const m = board.length;
    const n = board[0].length;

    // First pass: mark transitions using temporary states
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            let live = 0;

            for (let [x, y] of directions) {
                const ni = i + x, nj = j + y;
                if (
                    ni >= 0 && ni < m &&
                    nj >= 0 && nj < n &&
                    Math.abs(board[ni][nj]) === 1
                ) {
                    live++;
                }
            }

            if (board[i][j] === 1 && (live < 2 || live > 3)) {
                board[i][j] = -1; // Live to dead
            }

            if (board[i][j] === 0 && live === 3) {
                board[i][j] = 2; // Dead to live
            }
        }
    }

    // Second pass: finalize state updates
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            board[i][j] = board[i][j] > 0 ? 1 : 0;
        }
    }
};
```
## ＃140 - Set Matrix Zeroes 💥
#### Input/Output
```python
# Input
matrix = [[1, 1, 1], [1, 0, 1], [1, 1, 1]]

# Output
output = [[1, 0, 1], [0, 0, 0], [1, 0, 1]]
```

#### Intuition:
The goal here is to zero out the values that share a row or a column with an existing zero. To do this first save the indexes of the rows and columns that contain a zero, then zero those rows and columns out. Make sure to zero out only after the indices for both rows and columns have been stored. 

#### Approach:
- save the row numbers that contain zeros in a dict
- save the columns with zeros in a dict
- zero out all values in the rows and columns that contain a zero

#### Code:
```python
class Solution:
    def setZeroes(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        
        # Get all the rows with a zero
        rows_with_zero = {
            i for i in range(len(matrix))
            if any(matrix[i][j] == 0 for j in range(len(matrix[i])))
        }

        # Get all the columns with zero
        cols_with_zero = {
            j for j in range(len(matrix[0]))
            if any(matrix[i][j] == 0 for i in range(len(matrix)))
        }

        # Zero out rows
        for i in rows_with_zero:
            matrix[i] = [0 for _ in matrix[i]]

        # Zero out columns
        for row in matrix:
            for i in cols_with_zero:
                row[i] = 0

        return matrix
```
```javascript
var setZeroes = function(matrix) {
    const rowsWithZero = new Set();
    const colsWithZero = new Set();

    // Find all rows and columns that contain a zero
    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix[0].length; j++) {
            if (matrix[i][j] === 0) {
                rowsWithZero.add(i);
                colsWithZero.add(j);
            }
        }
    }

    // Zero out the rows
    for (let i of rowsWithZero) {
        for (let j = 0; j < matrix[0].length; j++) {
            matrix[i][j] = 0;
        }
    }

    // Zero out the columns
    for (let j of colsWithZero) {
        for (let i = 0; i < matrix.length; i++) {
            matrix[i][j] = 0;
        }
    }
};
```
## ＃141 - Integer to Roman 💥
#### Input/Output
```python
# Input
num = 3749
# Output
"MMMDCCXLIX"
```

#### Intuition:
The goal is to convert an integer to roman numerals. First, create a list pairing each unique roman numeral and its value - sorted from highest to lowest. Then, iterate through this list, if the integer is greater than the value of the roman numeral, add the roman numeral to the output string and subtract the value of the roman numeral from the integer. Continue this process until the integer is 0.

Note: To avoid creating new variables, the input integer is reused by subtracting the value of each output roman numeral as we go.

Note: Use a list as opposed to a dict for the roman numerals. Dictionary iteration order is not guaranteed. Because the order is important, use a list.

#### Approach:
- Create a list of each unique pair of roman numerals and their values, ordered from largest to smallest.
- Iterate through the list, if the target integer is greater than the value of the roman numeral, append that numeral to the results list and subtract the value of that numeral from the target integer.
- Advance to the next (lower) roman numeral only when the input is less than the numeral value. 

#### Code: 
```python
# Python
class Solution(object):
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        roman_list = [
            (1000, 'M'), (900, 'CM'),
            (500, 'D'), (400, 'CD'),
            (100, 'C'), (90, 'XC'),
            (50, 'L'), (40, 'XL'),
            (10, 'X'), (9, 'IX'),
            (5, 'V'), (4, 'IV'),
            (1, 'I')
        ]

        results = []

        for value, symbol in roman_list:
            while num >= value:
                results.append(symbol)
                num -= value

        return ''.join(results)
```
```javascript
// JavaScript
var intToRoman = function(num) {
    const values = [
        [1000, "M"], [900, "CM"], [500, "D"], [400, "CD"],
        [100, "C"], [90, "XC"], [50, "L"], [40, "XL"],
        [10, "X"], [9, "IX"], [5, "V"], [4, "IV"], [1, "I"]
    ];
    let result = '';
    for (const [value, symbol] of values) {
        while (num >= value) {
            result += symbol;
            num -= value;
        }
    }
    return result;
};
```
## ＃142 - Length of Last Word 💥
#### Input/Output
```python
# Input
s = "Hello World"

# Output
5
```

#### Intuition:
The goal here is to find the length of the last word. To do this, first 'clean up' any extra white spaces in the string, then isolate the word by splitting on the last white space. Once the word is isolated into its own variable, simply count the letters with len().  

Note: To avoid processing the entire sting, 'rsplit' and 'rstrip' are used to begin at the end of the list.

#### Approach:
- Remove the leading and trailing whitespaces with 'rstrip'
- Use rsplit(' ', 1)[-1] to begin splitting from the end, split only once, and save the last chunk as a variable (last_word). 
- Use len() to get the length of the word

#### Code:   
```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """

        s = s.rstrip()

        last_word = s.rsplit(' ', 1)[-1]

        word_length = len(last_word)


        return word_length
```
```javascript
    var lengthoflastword = function(s) {
        s = s.trimEnd();

        const lastSpaceIndex = s.lastIndexOf(' ');
        const lastword = lastSpaceIndex === -1 ? s : s.slice(lastSpaceIndex + 1);

        return lastword.length;
    }
```
## ＃143 - Longest Common Prefix 💥
#### Input/Output
```python
# Input
strs = ["flower","flow","flight"]
# Output
"fl"
```

#### Intuition:
The goal is to find the longest common prefix across every word in the list. To do this, compare the first word to the remaining words to see if they match, beginning with the first letter, then the first two letters, ect. to find the longest common prefix. At each iteration, see if all the other words begin with the same prefix, if so, the 'longest_prefix' variable is updated, if not, the current 'longest_prefix' variable is returned. 

Note: Using the first word to iterate over avoids needing to sort the list.

#### Approach:
- Iterate over each incrementing prefix in the first word.
- For each prefix, iterate over all remaining words to see if they contain the prefix. If not, it returns the current longest prefix, if so, it updates the ‘longest_prefix’ variable and repeats the process with the next (longer) prefix.

#### Code: 
```python
class Solution(object):
    def longestCommonPrefix(self, strs: list = []) -> str:
        """
        :type strs: List[str]
        :rtype: str
        """

        longest_prefix = ''

        # Loop over each letter in the first word
        for i in range(0, len(strs[0])):
            #  Prefix is a str = to the first letter through the current letter
            prefix = strs[0][0:i+1]

            # Loop over the remaining words
            for j in range(1, len(strs)):

                # See if the word shares the prefix
                if strs[j][0:i+1] != prefix:

                    # Exit the loop if it doesnt match
                    return longest_prefix
            
            # If if gets through each word, update the longest_prefix string
            longest_prefix = prefix

        return longest_prefix
```
```javascript
longestCommonPrefix(strs = []) {
    let longest_prefix = '';

    if strs.length === 0 return longest_prefix;

    for (let i = 0; i < strs[0].length; i++) {

        const prefix = strs[0].substring(0, i+1);

        for (let j = 0; j < strs.length; j++) {
            if (strs[j].substring(0, i+1) !== prefix) {
                return longest_prefix;
            }
        }

    longest_prefix = prefix;
    }

    return longestPrefix;
}
```
## ＃144 - Reverse Words in a String 💥
#### Input/Output
```python
# Input
s = "the sky is blue"

# Output
"blue is sky the"
```

#### Intuition:
The goal is to return all the words in the list without the extra whitespaces and in reverse order. To do this 1. Remove leading and trailing whitespaces 2. Split the string at each internal space and return non-empty words as a list in reverse order 3. Rejoin these words into a string.

Note: Use [::-1] to reverse sort the list without creating an additional variable. 

#### Approach:
- Use 'strip' to remove leading and trailing spaces.
- Use 'split()[::-1]' to create a list of words in reverse order. The trick is to sort by '-1' to easily satisfy the reverse order constraint. This will also handle any repeated space between words.
- Simply use join with ' ' to create the output string. 

#### Code:
```python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """

        s = s.strip()

        word_list = s.split()[::-1]

        reverse_string = ' '.join(word_list)

        return reverse_string

```
```javascript
reverseWords(s) {

    s = String(s).trim();

    const word_list = s.split(/\s+/).reverse();

    const reverse_string = word_list.join(' ');

    return reverse_string;
}
```
## ＃145 - Zigzag Conversion 💥
#### Input/Output
```python
# Input
s = "PAYPALISHIRING"

# Output
"PAHNAPLSIIGYIR"
```

#### Intuition:
The goal is to rearrange the string. This will be done by iterating over the string in a specific way and adding each letter to a new string as we go. To do this, iterate by row adding the letters needed before moving onto the next row.

#### Approach:
- Iterate one row at a time
- For each row, iterate over the string begining with the index where (index = row number - 1) and skipping over indexes with an interval equal to 2(n-1) where n is the number of rows. For the middle rows, also add the indexes  (2(n-1) - (2i)) greater than the index at each interval, this adds the diagnal letters. 

#### Code:
```python
def convert(self, s, numRows):
    """
    :type s: str
    :type numRows: int
    :rtype: str
    """
    if numRows == 1:
        return s

    final_string = ''

    for i in range(numRows):
        for j in range(i, len(s), 2*(numRows-1)):
            final_string+=s[j]
            if (i>0 and i<numRows-1 and j + 2*(numRows-1) - (2*i) < len(s)):
                final_string+=s[j + 2*(numRows-1) - (2*i)]

    return final_string
```
```javascript
var convert = function(s, numRows) {
    if (numRows === 1) return s;

    let finalString = '';

    for (let i = 0; i < numRows; i++) {
        for (let j = i; j < s.length; j += 2 * (numRows - 1)) {
            finalString += s[j];
            let diag = j + 2 * (numRows - 1) - 2 * i;
            if (i > 0 && i < numRows - 1 && diag < s.length) {
                finalString += s[diag];
            }
        }
    }

    return finalString;
};
```
## ＃146 - Valid Sudoku 💥
#### Input/Output
```python
# Input
board = [
["5","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]]

# Output
true
```

#### Intuition:
The goal is to check if the sudoku board is valid. To check, handle each of the three features seperately (rows, columns, squares). As soon as a a duplicate is found, exit. 

#### Approach:
- For each row check if the len of the values is equal to the set (check for duplicates) if so exit, if not continue.
- Next do the same for each column
- Finally check the squares.

#### Code:
```python
def isValidSudoku(self, board):

    # Check rows
    for row in board:
        values = [num for num in row if num != "."]
        if len(values) != len(set(values)):  # Ignore empty cells
            return False

    # Check columns
    for i in range(9):  # Since it's a 9x9 board
        col = [board[row][i] for row in range(9) if board[row][i] != "."]
        if len(col) != len(set(col)):
            return False

    # Check 3x3 sub-boxes
    for row_start in [0, 3, 6]:  
        for col_start in [0, 3, 6]:  
            square = [
                board[i][j] for i in range(row_start, row_start + 3)
                            for j in range(col_start, col_start + 3) 
                            if board[i][j] != "."
            ]
            if len(square) != len(set(square)):
                return False

    return True  # If no duplicates found, the Sudoku board is valid
```
```javascript
var isValidSudoku = function(board) {

    // Check rows
    for (let row of board) {
        let values = row.filter(num => num !== ".");
        if (new Set(values).size !== values.length) {
            return false;
        }
    }

    // Check columns
    for (let i = 0; i < 9; i++) {
        let col = [];
        for (let row = 0; row < 9; row++) {
            if (board[row][i] !== ".") {
                col.push(board[row][i]);
            }
        }
        if (new Set(col).size !== col.length) {
            return false;
        }
    }

    // Check 3x3 sub-boxes
    for (let rowStart of [0, 3, 6]) {
        for (let colStart of [0, 3, 6]) {
            let square = [];
            for (let i = rowStart; i < rowStart + 3; i++) {
                for (let j = colStart; j < colStart + 3; j++) {
                    if (board[i][j] !== ".") {
                        square.push(board[i][j]);
                    }
                }
            }
            if (new Set(square).size !== square.length) {
                return false;
            }
        }
    }
    return true;
};
```
## ＃147 - Find the Index of the First Occurrence in a String 💥
#### Input/Output
```python
# Input
haystack = "sadbutsad"
needle = "sad"

# Output
0
```

#### Intuition:
My favorite solution so far. The goal here is to find the first occurance of a substring in a main string. .find() & .index() both return the first occurance of the input, but .find() returns -1 when not found, while .index() return an error messge. Using find() avoids the if-then logic needed when the needle doesnt exist in the haystack.
HINT: Use .find() when you're not sure if the string exists, and use .index() when you're sure it does and want an error otherwise.

#### Approach:
- use haystack.find(needle) in the return statement and we good.

#### Code:
```python
def strStr(self, haystack: str, needle: str) -> int:
    return haystack.find(needle)
```
```javascript
function strStr (haystack, needle) {
    return haystack.indexOf(needle);
}
```
## ＃148 - Spiral Matrix 💥
#### Input/Output
```python
# Input
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]]

# Output
[1,2,3,6,9,8,7,4,5]
```

#### Intuition:
The goal here is to return a string of the matrix values in a sprial clockwise order. Break the issue into 4 parts, the top row, the last column, the last row, and the first column. One at a time, extract the numbers as a string and remove them from the matrix. Rotate through each step until the matrix is empty. 

#### Approach:
- iterate over values in the first row, append them to results and remove them from the matrix. 
- iterate over the last column, append them to results and remove them from the matrix.
- iterate over last row in reverse order, append them to results and remove them from the matrix.
- iterate over the first column in reverse order, append them to results and remove them from the matrix.
- repeat

#### Code:
```python
class Solution(object):
    def spiralOrder(self, matrix):
        output_list = []
        step = 1

        while matrix and matrix[0]:

            if step == 1:

                for i in matrix[0]:
                    output_list.append(i)

                del(matrix[0])
                step += 1
                continue

            if step == 2:

                j = len(matrix[0]) -1

                for i in range(0, len(matrix)):
                    output_list.append(matrix[i][j])

                    del(matrix[i][j])

                step += 1
                continue

            if step == 3:

                for i in matrix[-1][::-1]:
                    output_list.append(i)

                del(matrix[-1])
                step += 1
                continue

            if step == 4:

                for i in range(len(matrix) - 1, -1, -1):

                    output_list.append(matrix[i][0])

                    del(matrix[i][0])
                step = 1
                continue

        return output_list
```
```javascript
function spiralOrder(matrix) {
    let outputList = [];
    let step = 1;

    while (matrix.length && matrix[0].length) {
        if (step === 1) {
            // Traverse top row
            outputList.push(...matrix[0]);
            matrix.shift();
            step++;
            continue;
        }

        if (step === 2) {
            // Traverse right column
            for (let i = 0; i < matrix.length; i++) {
                outputList.push(matrix[i][matrix[i].length - 1]);
                matrix[i].splice(matrix[i].length - 1, 1);
            }
            step++;
            continue;
        }

        if (step === 3) {
            // Traverse bottom row in reverse
            outputList.push(...matrix[matrix.length - 1].reverse());
            matrix.pop();
            step++;
            continue;
        }

        if (step === 4) {
            // Traverse left column bottom to top
            for (let i = matrix.length - 1; i >= 0; i--) {
                outputList.push(matrix[i][0]);
                matrix[i].splice(0, 1);
            }
            step = 1;
            continue;
        }
    }

    return outputList;
}
```
## ＃149 - Rotate Image 💥
#### Input/Output
```python
# Input
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]]

# Output
[
[7,4,1],
[8,5,2],
[9,6,3]
]
```

#### Intuition:
The goal is to rotate the matrix. To do this reverse the order of the rows and then transpose the matrix so each row becomes a column.

#### Approach:
- A[::-1] to reverse column order
- zip(*A[::-1]) to transposes the rows into columns
- map(list, ) to convert tuples back to list

#### Code:
```python
def rotate(A):
    A[:] = map(list, zip(*A[::-1]))

    return A
```
```javascript
function rotate(A) {
    const n = A.length;

    // Reverse the rows
    A.reverse();

    // Transpose: create a new array with rotated values
    const rotated = [];

    for (let i = 0; i < n; i++) {
        rotated.push([]);
        for (let j = 0; j < n; j++) {
            rotated[i].push(A[j][i]);
        }
    }

    // Copy back into A (in-place)
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            A[i][j] = rotated[i][j];
        }
    }

    return A;
}
```

## ＃150 - Text Justification 💥
#### Input/Output
```python
# Input
words = ["This", "is", "an", "example", "of", "text", "justification."]
maxWidth = 16 

# Output
[
"This    is    an",
"example  of text",
"justification.  "]
```

#### Intuition:
Loop through each word counting the letters as you go. Add each word to a list until the count is greater than 16. Before adding this word, loop through each word adding a space until no more are needed.

#### Approach:
- Iterate over each word
- Count the amount of letters of each word until you go over 16, 
- For each of these words loop through and add a space to the end, 
- iterate once for each space needed to add
- Join the edited words into a string and add to the results list. 
- repeat until you run out of words and line join the strings together

#### Code:
```python
def fullJustify(self, words, maxWidth):
    res, cur, num_of_letters = [], [], 0
    for w in words:
        if num_of_letters + len(w) + len(cur) > maxWidth:
            for i in range(maxWidth - num_of_letters):
                cur[i%(len(cur)-1 or 1)] += ' '
            res.append(''.join(cur))
            cur, num_of_letters = [], 0
        cur += [w]
        num_of_letters += len(w)
    return res + [' '.join(cur).ljust(maxWidth)]
```
```javascript
var fullJustify = function(words, maxWidth) {

    const res = [];
    let cur = [];
    let numOfLetters = 0;

    for (const w of words) {
        if (numOfLetters + w.length + cur.length > maxWidth) {
            for (let i = 0; i < maxWidth - numOfLetters; i++) {
                // Add space to word at index i % (cur.length - 1 or 1)
                const index = cur.length > 1 ? i % (cur.length - 1) : 0;
                cur[index] += ' ';
            }
            res.push(cur.join(''));
            cur = [];
            numOfLetters = 0;
        }
        cur.push(w);
        numOfLetters += w.length;
    }

    // Last line: join with single spaces, then pad right with spaces to maxWidth
    res.push(cur.join(' ').padEnd(maxWidth, ' '));
    return res;
};
```

# Workspace Set-up

```bash
# Clone the repository
git clone https://github.com/joel-day/LeetCode-Workspace.git

# Move into the local repository
cd LeetCode-Workspace

# Create the virtual environment
uv venv .venv

# Activate the virtual environment
source .venv\bin\activate # Mac/Linux
.venv\Scripts\activate   # Windows

# Sync environment based on dependencies in top-level pyproject.toml file
uv sync

# (OPTIONAL) Sync environment based on dependencies across all packages' pyproject.toml files
uv sync --all-packages
```
## Flashcards
- Flashcards are stored in the 'data/raw/qa.xlsx' excel file.
- Use the "add_flashcard.ipynb" notebook to add cards.
- Run the bash shortcut below in the terminal to open the flashcard UI.
```bash
flashcards
``` 

## Bash Scripts
- 'flake8 .'  Use for:   PEP8 compliance.  Python solutions are added to 'helpers/helper.py' to use with flake8. 
- 'browser'   Use for:   Saving time.      Loads ChatGPT and LeetCode in the browser. 
```bash
flake8 .
browser
```
