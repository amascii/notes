#### Exercise 13 - Experimenting recursion
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
f :: (Integral a) => a -> [a]
f x
  | x == 0 = [0]
  | even x = x : f (x - 2)
  | otherwise = f (x - 1)
f x = aux x [0]
  where
  aux :: (Integral a) => a -> [a] -> [a]
  aux x res
    | x == 0 = res
    | even x = aux (x - 2) (x : res) 
    | otherwise = aux (x - 1) res
-- 2                

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

```
