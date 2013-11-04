# 3 List Monad ���

## dice

```haskell
import Data.List
import Control.Monad

dice :: [Int] -> Int -> Int -> [Int]
dice _ _ 0 = return 0
dice as g n = sort $ nub $ do
    x <- dice as g (n-1)
    a <- as
    if x==g || x+a>=g then return g else
        if x+a<0 then return 0 else return (x+a)
```

���X�g���i�h�̊�{�I�Ȏg�����ł��B�����A���ʂ��d���Ȃ������ɕ��ׂ邽�߂� nub �ŏd������菜�������� sort �ŏ����ɕ��ׂĂ��܂��B

���Ȃ݂ɁA�~���ɂ������ꍇ�� sortBy (flip compare) �Ƃ���΂悢�ł��B

## main

```haskell
main = do g <- readLn
          n <- readLn
          k <- readLn
          as <- replicateM k readLn
          print $ dice as g n
```
