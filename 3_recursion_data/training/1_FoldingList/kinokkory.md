# 1 Folding List ���

## length

```haskell
length :: [a] -> Int
length = foldr (\_ n -> n+1) 0
```

���̂悤�ɂ������܂��B

```haskell
length :: [a] -> Int
length = foldl (\n _ -> n+1) 0
```

## map

```haskell
map :: (a -> b) -> [a] -> [b]
map f = foldr (\a bs -> f a : bs) []
```

����� O(n) �ł��B

���̂悤�ɂ������܂����AO(n^2) �ƂȂ�����������ł��B

�u[x1,x2,...,xn]++[y1,y2,...,ym]�v�̌v�Z�ʂ� O(n) �ł��邱�Ƃɒ��ӂ��܂��傤�B

```haskell
map :: (a -> b) -> [a] -> [b]
map f = foldl (\bs a -> bs ++ [f a]) []
```

��ʂɁA���X�g��̑����̍ċA�֐���foldr�Ŏ�������ق����悢�ł��Bfoldr�̂ق������X�g�̍\���ɑ΂��đf���ȕ��@������ł��B

## reverse

```haskell
reverse :: [a] -> [a]
reverse = foldl (\as a -> a : as) []
```

����� O(n) �ł��Bfoldl�Ŏ�������ق��������̂����H�ȗ�ł��B

���̂悤�ɂ������܂����AO(n^2) �ƂȂ�����������ł��B

```haskell
reverse = foldr (\a as -> as ++ [a]) []
```

## filter

```haskell
filter :: (a -> Bool) -> [a] -> [a]
filter f = foldr (\a as -> if f a then a:as else as) []
```

����� O(n) �ł��B

���̂悤�ɂ������܂����AO(n^2) �ƂȂ�����������ł��B

```haskell
filter :: (a -> Bool) -> [a] -> [a]
filter f = foldr (\as a -> if f a then as++[a] else as) []
```

## subsequences

```haskell
subsequences :: [a] -> [[a]]
subsequences = foldr (\a ass -> concatMap (\as -> [as,a:as]) ass) [[]]
```

����Ōv�Z�ʂ� O(n * 2^n) �ɂȂ�܂��B

���������̌v�Z�ʂ͔ߌ��I�ɒx���Ȃ�܂��B

```haskell
subsequences :: [a] -> [[a]]
subsequences = foldl (\a ass -> ass ++ map (++[a]) ass) [[]]
```
