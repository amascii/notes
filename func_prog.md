## Problems

#### Exercise 1 - Evaluation and prefix notation
Evaluate the following expressions and convert them to the equivalent expression in prefix notation.

```haskell
-- 1
2 ^ 4 - 1

--answer
(-) ((^) 2 4)1
= 15

-- 2
2 * 3 * (5 - 1)

-- answer
(*) 2 ((*) 3 ((-) 5 1))
= 24

-- 3
2 + 1 + 3 / 4

-- answer
(+) 2 ((+) 1 ((/) 3 4))
= 3.75

-- 4
(3 - 1) / (4 + 2)

-- answer
(/) ((-) 3 1) ((+) 4 2)
= 0.33...
```

#### Exercise 2 - Data types
```haskell
--answer
rate = 120
:t rate
> rate :: Integer

rate :: Float
> rate :: Float

result = rate * 3.40
:t result
> result :: Float
```

#### Exercise 3 - Scope
Evaluate and find x.

```haskell
-- 1
a = 1
x = a + 1

-- answer
= 2

-- 2
a = 1
x = a + 1 where a = 0

-- answer
= 1

-- 3
a = 1
x = a + 1 where a = a + 2 where a = 3

-- answer
= 6

-- 4
a = 1
x = a + let a = 2 in a + 1

-- answer
= 4
```

#### Exercise 4 - Functions
Evaluate the following expressions.

```haskell
--1
f x = x * x
f 4

-- answer
= 16

-- 2
f = (+)
f 2 1

-- answer
= 3

-- 3
f = \x -> x * x
f 2

-- answer
= 4

-- 4
f g = \x y -> 1 + g x y
(f (+)) 2 1

-- answer
= 4
```

#### Exercise 5 - Currying
Evaluate and answer the questions.

1.
```haskell
f x y = x * y  
-- Q: what is f? 
-- A: a binary function that multiplies two numbers

g = f 2
-- Q: what is g?
-- A: f with only the first argument defined

g 3

-- answer
= 6
```

2.
```haskell
p x y z = x + y - z 
-- Q: what is p?
-- A: a ternary function

p 5 4
-- Q: what is returned?
-- A: an error, not enough arguments
-- A: a unary function that subtracts the given parameter from 9

q = p 1
-- what is q?
-- A: a binary function that adds its first parameter to 1 then subtract the second parameter

r = q 2
-- what is r?
-- A: a unary function that subtracts the given parameter from 3

r 3

-- answer
= 0
```

#### Exercise 6 - Contracts
Give a possible signature for the following functions.
```haskell
-- 1
f x y = x == y

-- answer
f :: (Eq a) => a -> a -> Bool

-- 2
g x y = x <= y

-- answer
g :: (Ord a) => a -> a -> Bool
```

#### Exercise 7 - Lists
Evaluate the following expressions.
```haskell
1:[]            -- 1 [1]
1:[True]        -- 2 error
[1] : [[2],[2]] -- 3 [[1],[2],[2]]
[0,'a','b']     -- 4 error
'h':"ello"      -- 5 "hello"
"h":"ello"      -- 6 error
[]:[]:[]        -- 7 [[],[]]
```

#### Exercise 8 - Lists and signatures
Write the signature of the list accessor function `tail`.
```haskell
tail :: [a] -> [a]
```

#### Exercise 9 - Tuples
Evaluate the following expressions.
```haskell
1:[2,3]           -- 1 [1,2,3] 
1:(2,3)           -- 2 error (tuples are immutable)
(,) 1 2           -- 3 (1,2)
(,) 1 2 3         -- 4 error
(1,2,False)       -- 5 (1,2,False)
[(1,2),(9,False)] -- 6 error (elements of list can't have different types)
([1,2],[True])    -- 7 ([1,2],[True]) (anything goes in tuples)
```

#### Exercise 10 - Tuple and signatures
Write the signature of the tuple accessor function `snd`.
```haskell
snd :: (a, b) -> b
```

#### Exercise 11 - List comprehension
Solve the following problems using list comprehension.
```haskell
-- 1 N
[1..]

-- 2 (N,N)
[(i, i) | i <- [1..] ]

-- 3 (N,-N)
[(i, -i) | i <- [1..] ]

-- 4 even (N, -N)
[(i, -i) | i <- [1..], even i ]
[(i, -i) | i <- [2,4..]]

-- 5 pairs of N whose sum is even
[(i, j) | i <- [1..], j <- [1..], even (i+j) ]
```

#### Exercise 12 - Relations
Evaluate the following expressions.
```haskell
1 < 2                   -- 1 True
(1 < 2) && (3 > 4)      -- 2 False
(1 < 2) || (3 > 4)      -- 3 True
not (2 == 2) || (1 < 2) -- 4 True
False && ...            -- 5 False
True || ...             -- 6 True
```

#### Exercise 13 - Recursion
Evaluate the following expressions.

1.
```haskell
f x = if x == 0
        then 0
        else x + f (x - 1)
f 3

-- answer
3+(2+(1+0))
= 6
```

2. 
```haskell
g x = if x > 8
        then 1
        else x + g (2 * x)
f 2

-- answer
2+(4+(8+1)
= 15
```

#### Exercise 14 - Experimenting list recursion
Evaluate the following expressions.

1.
```haskell
f :: (Eq a, Num a) => [a] -> a
f x = if x == []
        then 0
        else 2 * (head x) + f (tail x)
f [1, 2, 3]

-- answer
2*1 + 2*2 + 2*3
= 12
```

2.
```haskell
g :: (Eq a) => [a] -> [a]
g x
  | x == 0 = []
  | otherwise = head x : g (tail x)
g [1, 2, 3]

-- answer
1 : 2 : 3 : []
= [1, 2, 3]
```

#### Exercise 15 - Experimenting list recursion
1. Write a function `f x` that returns 
the list of all the even integers in the interval [0,x]. (Use `even`)
```haskell
-- answer
f :: (Integral a) => a -> [a]
f x
  | x == 0 = [0]
  | even x = x : f (x - 2)
  | otherwise = f (x - 1)
```

2. Write a function `g l` whose input is a list of integers and
which returns the list containing the corresponding opposite integers (i.e. return `-x` for `x`)
```haskell
-- answer
g :: (Integral a) => [a] -> [a]
g l
  | l == [] = []
  | otherwise = - (head l) : g (tail l)
```

#### Exercise 16 - Experimenting tail recursion
1. Rewrite Exercise 14 using tail recursion.
```haskell
-- answer
-- 1
f x = aux x 0
  where
  aux :: Integer -> Integer -> Integer
  aux x res = if x == 0
                then res
                else aux (x - 1) (res + x)

-- 2                
g x = aux x 1
  where
  aux :: Integer -> Integer -> Integer
  aux x res
    | x > 8 = res
    | otherwise = aux (2 * x) (res + x)
```

2. Rewrite Exercise 15 using tail recursion.
```haskell
-- answer
-- 1
f :: Int -> [Int]
f x = aux x []
  where
  aux :: Int -> [Int] -> [Int]
  aux x res
    | x == 0 = 0 : res
    | even x = aux (x - 2) (x : res) 
    | otherwise = aux (x - 1) res
-- 2                
-- answer
g :: [Int] -> [Int]
g l = aux l []
  where
  aux :: [Int] -> [Int] -> [Int]
  aux l res
    | l == [] = reverse res
    | otherwise = aux (tail l) (- (head l) : res)
```

#### Exercise 17 - Experimenting program termination
Identify under which conditions the following programs terminate.

1.
```haskell
-- Computing the product x * (x+1) * (x+2) * ...
f x = if x == 0
        then 1
        else x * f (x + 1)
        
-- answer
x <= 0
```

2.
```haskell
-- Computing the sum x + (x+2) + ...
g x = if x == 10
  then 0
  else x + g (x + 2)
  
-- answer
even x, x <= 10
```

3.
```haskell
-- Computing the sum x + (x+2) + ...
h x
  | x == 10 = 0
  | x == 11 = 0
  | otherwise x + h (x + 2)
  
-- answer
x <= 9
```

#### Exercise 18 - Experimenting pattern matching
1. Evaluate.
```haskell
f 1 _ = "result1"
f _ _ = "result2"
f _ 1 = "result3"
f 2 3
f 2 1
f 1 1

-- answer
= "result2"
= "result2"
= "result1"
```

2. Evaluate.
```haskell
g True x = x
g False 0 = -1
g _ x = x + 1
g False 1
g True 0
g False 0

-- answer
= 2
= 0
= -1
```

#### Exercise 19 - Experimenting pattern matching (matching tuples and lists)
Solve the following exercises using pattern matching (w/ function signatures). 

Write a function that
1. returns `True` only if a string starts with the character `'A'`.
```haskell
-- answer
f :: [Char] -> Bool
f ('A':_) = True
f _ = False
```

2. increments by one the values of a pair (i.e. 2-tuple).
```haskell
-- answer
f :: (Num a, Num b) => (a, b)
f (a, b) = (a + 1, b + 1)
```

3. reverts the order of a pair's elements.
```haskell
-- answer
f :: (a, b) -> (b, a)
f (a, b) = (b, a)
```

4. takes two pairs as arguments, and that returns a 4-tuple merging the values of the pair arguments. E.g. `f (2, 5) (True, 0)` returns `(2, 5, True, 0)`.
```haskell
-- answer
f :: (a, b) -> (c, d) -> (a, b, c, d)
f (a, b) (c, d) = (a, b, c, d)
```

#### Exercise 20 - Experimenting pattern matching and recursion
Using pattern matching, write a function taking a parameter `n` and calculating the sum of 
1. the natural numbers `1 + 2 + ... + n`.
```haskell
-- answer
f :: Integer -> Integer
f 1 = 1
f n = n + f (n - 1)
```
2. the `n` first even numbers `0 + 2 + 4 + ...`
```haskell
-- answer
f :: Integer -> Integer
f 1 = 0
f n = 2*(n-1) + f (n - 1)
```

#### Exercise 21 - Experimenting pattern matching and list recursion
Using pattern matching, write a function `g l` whose input is a list of integers and that returns a list containing the corresponding opposite integers. Next, redefine the function `g` to rely on `map` instead.
```haskell
-- answer
g :: [Int] -> [Int]
g [] = [] 
g l = - (head l) : g (tail l)

g :: [Int] -> [Int]
g l = map (\x -> -x) l
```

#### Exercise 22 - Experimenting list processing with folding
Using folding, write a function
1. `append l` whose unique parameter is a list of lists, and that returns the concatenation of these lists.
```haskell
-- answer
append :: [[a]] -> [a]
append l = foldl (++) [] l
```

2. `expt l` that calculates the exponentiation `u1**u2** ...` of the list elements `u1, u2 ...`
```haskell
-- answer
expt :: [Integer] -> Integer
expt l = foldr (\x acc -> x ^ acc) 1 l
```

## Applications
#### Sorting algorithms
```haskell
-- insertion sort
insert :: (Ord a) => a -> [a] -> [a]
insert a [] = [a]
insert a l@(x:xs) 
	| a <= x = a : l
	| otherwise = x : insert a xs

insertion_sort :: (Ord a) => [a] -> [a]
insertion_sort [] = []
insertion_sort (x:xs) = insert x (insertion_sort xs) 

-- merge sort
merge :: (Ord a) => [a] -> [a] -> [a]
merge l1 [] = l1
merge [] l2 = l2
merge l1@(x:xs) l2@(y:ys)
	| x < y = x : merge xs l2
	| x > y = y : merge l1 ys
	| otherwise = x : y : merge xs ys

merge_sort :: (Ord a) => [a] -> [a]
merge_sort [] = []
merge_sort [x] = [x]
merge_sort l = merge (merge_sort left) (merge_sort right)
        where (left, right) = splitAt (quot (length l) 2) l

-- quick sort
quick_sort :: (Ord a) => [a] -> [a]
quick_sort [] = []
quick_sort (x:xs) = quick_sort [i | i <- xs, i <= x] ++ [x] ++ quick_sort [i | i <- xs, i > x]
```

```haskell
-- exercise 20 w/ tail recursion
-- 1
f :: Int -> Int
f n = aux n 0 
	where
	aux 0 res = res
	aux n res = aux (n - 1) (res + n)
-- 2	
f :: Int -> Int
f n = aux n 0
	where
	aux 1 res = res 
	aux n res = aux (n - 1) (2*(n-1) + res)
	
-- foldl execution trace
foldl (+) 0 [1,2,3]
foldl (+) ((+) 0 1) [2,3]
foldl (+) 1 [2,3]
foldl (+) ((+) 1 2) [3]
foldl (+) 3 [3]
foldl (+) ((+) 3 3) []
foldl (+) 6 []
6
-- foldr execution trace
foldr (:) [] [1,2,3]
(:) 1 (foldr (:) [] [2,3])
(:) 1 ((:) 2 (foldr (:) [] [3]))
(:) 1 ((:) 2 ((:) 3 (foldr (:) [] [])))
(:) 1 ((:) 2 ((:) 3 []))
(:) 1 ((:) 2 [3])
(:) 1 [2,3]
[1,2,3]
```

## Report
```haskell
[1,2,3] -> [[1,2,3], [1,3,2], ...]
perm (x:xs) perm xs
```
