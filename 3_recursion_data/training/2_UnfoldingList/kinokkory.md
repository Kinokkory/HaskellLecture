# 2 Unfolding List ���

## map

```haskell
map :: (a -> b) -> [a] -> [b]
map f = unfoldr (\as -> if null as then Nothing else Just (f (head as), tail as))
```

�I���������l����΂��������ł��B

## replicate

```haskell
replicate :: Int -> a -> [a]
replicate n a = unfoldr (\n -> if n==0 then Nothing else Just (a,n-1)) n
```

�I���������l����΂��������ł��B

## fib

```haskell
fib :: [Int]
fib = unfoldr (\(a,b) -> Just (a,(b,a+b))) (1,1)
```

�������X�g������̂ŁA�������̊֐��ł͂����� Just ... ��Ԃ����ƂɂȂ�܂��B
