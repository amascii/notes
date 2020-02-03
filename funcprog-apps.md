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
