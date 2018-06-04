---
layout: post
title:  "Weekly Contest 87"
date:   2018-06-01 22:00:00
categories: leetcode
---


## Problem Information

> * Link: [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/description/)
> * Source: LeetCode
> * Difficulty: Easy
> * Description:
```
Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.
```

## Solution
1. Go through S and T seperately and simplify them based on the rules given. Compare the simplified result.

## Complexity Analysis
Time complexity: O(M + N). 

## Details
1. S and T could be empty
2. There may be backspace for empty string

## AC Code

``` python
class Solution:
    def backspaceCompare(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: bool
        """
        
        if not S or not T:
            return True
        
        s = ''
        t = ''
        
        for i in range(len(S)):
            if S[i] != '#':
                s += S[i]
            else:
                if s == '':
                    pass
                else:
                    s = s[:-1]
        
        for j in range(len(T)):
            if T[j] != '#':
                t += T[j]
            else:
                if t =='':
                    pass
                else:
                    t = t[:-1]
                    
        print(s, t)
        
        return (s == t)
                    
```

## Problem Information

> * Link: [Longest Mountain in Array](https://leetcode.com/contest/weekly-contest-87/problems/longest-mountain-in-array/)
> * Source: LeetCode
> * Difficulty: Medium

> * Description:

```
Let's call any (contiguous) subarray B (of A) a mountain if the following properties hold:

	B.length >= 3
	There exists some 0 < i < B.length - 1 such that B[0] < B[1] < ... B[i-1] < B[i] > B[i+1] > ... > B[B.length - 1]
	(Note that B could be any subarray of A, including the entire array A.)

	Given an array A of integers, return the length of the longest mountain. 

	Return 0 if there is no mountain.
```

## Solution
1. Go through A and compare every connecting height and decide whether they follows the rule of generating a mountain.
2. Here I use d as direction, d = 1 means increasing, d = -1 means dicreasing and d = 0 means keeping the height.

## Complexity Analysis
Time complexity: O(N). 

## Details
1. The first given height has to be special treated
2. If the last given height is belonging to a "mountain", it may be ignored. I add a dummy end to the list to make the real end count.

## AC Code

``` python
class Solution:
    def longestMountain(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        
        if not A:
            return 0
        
        if len(A) == 1:
            return 0
        
        res = 0
        count = 0
        d = 0
        A. append(10001)
        
        for i in range(len(A) - 1):
            if d == 0:
                if A[i] >= A[i + 1]:
                    count = 0
                else:
                    d = 1
                    count = 1

            elif d == 1:
                if A[i] < A[i + 1]:
                    count += 1
                elif A[i] > A[i + 1]:
                    count += 1
                    d = -1
                else:
                    d = 0
                    count = 0

            else:
                if A[i] > A[i + 1]:
                    count += 1
                elif A[i] < A[i + 1]:
                    count += 1
                    res = max(res, count)
                    count = 1
                    d = 1
                else:
                    count += 1
                    res = max(res, count)
                    d = 0
                    count = 0
            # print(A[i], A[i + 1], d, count, res)
                    
        return res                  
```

## Problem Information

> * Link: [Hand of Straights](https://leetcode.com/contest/weekly-contest-87/problems/hand-of-straights/)
> * Source: LeetCode
> * Difficulty: Medium
> * Description:

```
Alice has a hand of cards, given as an array of integers.

Now she wants to rearrange the cards into groups so that each group is size W, and consists of W consecutive cards.

Return true if and only if she can.
```

```

## Solution
1. First I have to check whether the cards can be seperate into groups.
2. If it can be seperate, I start from the smallest card and check whether it can generate a contiguous group. If not, then break, if so, then remove the selected cards and repeat the process

## Complexity Analysis
I am not sure about the time complexity.

## Details
1. I use dictionary to record the card frequency.

## AC Code

``` python
class Solution:
    def isNStraightHand(self, hand, W):
        """
        :type hand: List[int]
        :type W: int
        :rtype: bool
        """
        
        if not hand or not W:
            return False
        
        if len(hand) % W != 0:
            return False
        
        card_dict = {}
        
        for card in hand:
            card_dict[card] = card_dict.get(card, 0) + 1
            
        cards = list(card_dict.keys())
        cards.sort()
        
        while len(cards) > 0:
            start = cards[0]
            for i in range(W):
                if card_dict.get(start + i):
                    card_dict[start + i] -= 1
                    if card_dict[start + i] == 0:
                        del card_dict[start + i]
                else:
                    return False
            
            cards = list(card_dict.keys())
            cards.sort()
            
        return True            
```





[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

