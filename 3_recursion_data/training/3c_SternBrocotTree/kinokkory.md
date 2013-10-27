# 3c Stern-Brocot Tree ���

## sternbrocotTree

```haskell
sternbrocotTree :: BinaryTree Rational
sternbrocotTree = go (0,1) (1,1) (1,0)
    where go (a,b) (c,d) (e,f) =
              Bin (go (a,b) (a+c,b+d) (c,d)) (c%d) (go (c,d) (c+e,d+f) (e,f))
```

�P�ɍċA���邾���ł��B�����A1%0�Ƃł��Ȃ��̂ŁA�L�������^�v���ŕ\������Ƃ����H�v�����Ă��܂��B

## simplest

```haskell
simplest :: (Double,Double) -> Rational
simplest (a,b) = simplest' sternbrocotTree (a,b)
    where simplest' (Bin l x r) (a,b)
            | a'<=x&&x<=b' = x
            | b'<x = simplest' l (a,b)
            | x<a' = simplest' r (a,b)
            where a' = toRational a
                  b' = toRational b
```

�͈͂ɑ�����L�����̂����AStern-Brocot�؏�ł����΂�󂢈ʒu�ɂ�����̂������𖞂����Ƃ������Ƃ͖��炩�ł��傤�B

�����[���̓񐔂��͈͂ɑ����Ă���ꍇ�A���̓񐔂̋��ʂ̐e���邢�͑c����܂��͈͂ɑ����Ă���̂ŁA�P����Stern-Brocot�؂������炽�ǂ��Ă����Α��v�ł��B

���Ȃ݂ɓ��l�̋@�\�����֐��Ƃ��āAData.Ratio�ł�

```haskell
approxRational :: RealFrac a => a -> a -> Rational
```

����`����Ă��܂��B�����������Hoogle�ȂǂŎ��������Ă݂܂��傤�B

## rationals

```haskell
rationals :: Integer -> [Rational]
rationals k = rationals' sternbrocotTree k
    where rationals' (Bin l x r) k
            | denominator x + numerator x > k = []
            | otherwise = rationals' l k ++ [x] ++ rationals' r k
```

�C�ӂ̐ߓ_�ɂ��āA���̎q�͕K������ƕ��q�̘a���傫���Ȃ��Ă���̂ŁA�[���D��T��������΂����ł��B
