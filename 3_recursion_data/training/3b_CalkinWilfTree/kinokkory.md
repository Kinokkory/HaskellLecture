# 3b Calkin-Wilf Tree ���

## calkinwilfTree

```haskell
calkinwilfTree :: BinaryTree Rational
calkinwilfTree = go (1%1)
    where go x = Bin (go (m%(m+n))) x (go ((m+n)%n))
            where m = numerator x
                  n = denominator x
```

�P�ɍċA���邾���ł��B

## calkinwilfSeq

```haskell
calkinwilfSeq :: [Rational]
calkinwilfSeq = map top queue
    where queue = calkinwilfTree : walk queue
          walk (Bin l _ r : q) = l : r : walk q
          top (Bin _ x _) = x
```

queue��walk���ċA���Ă��ăp�b�ƌ����Ɩ󕪂���Ȃ��I�ƂȂ邩������Ȃ��̂ŁA�⑫���������Ă����܂��B

```haskell
t1 = Bin t2 x1 t3
t2 = Bin t4 x2 t5
t3 = Bin t6 x3 t7
...
```

�Ƃ����f�[�^�\���ɂȂ��Ă���Ƃ��܂��B

```haskell
q1 = t1 : walk q1
walk (Bin l _ r : q) = l : r : walk q
```

�Ə�����Ă���Ƃ��āAq1�����ɓW�J���Ă����܂��傤�B

```haskell
q1 = t1 : walk q1
   = t1 : t2 : t3 : walk q2
          |______q2_______|
   = t1 : t2 : t3 : t4 : t5 : walk q3
               |_________q3_________|
   = t1 : t2 : t3 : t4 : t5 : t6 : t7 : walk q4
                    |___________q4____________|
   = ...
```

�ȉ����l�ɑ����Ă����܂��B�܂��ɃL���[�̂悤�ɂȂ��Ă���̂�������Ǝv���܂��B

## calkinwilfSeqAnother

```haskell
calkinwilfSeqAnother :: [Rational]
calkinwilfSeqAnother = concat $ levels calkinwilfTree
    where levels (Bin l x r) = [x] : zipWith (++) (levels l) (levels r)
```

calkinwilfSeq�̕ʉ��ł��B

levels�ł͖؂�[�����Ƃɕ��������X�g�̃��X�g������Ă��܂��Blevels�͂��ꂢ�ɍċA�I�ɏ����邱�Ƃ��킩��܂��B

���Ƃ́A���̃��X�g�����ׂĂȂ����킹��Ε��D�摖���̊����ł��I

���Ȃ݂ɁA���X�g�̌����ŏ����]���Ɏ��Ԃ�H���̂ŁA�������X�g���g���΂������������Ȃ�܂��B

## calkinwilfGet

```haskell
calkinwilfGet :: Int -> Rational
calkinwilfGet n =  top $ foldr func calkinwilfTree $ digits n
    where digits 1 = []
          digits n = mod n 2 : digits (div n 2)
          func 0 (Bin l _ _) = l
          func 1 (Bin _ _ r) = r
```

digits��n���i���̌��ɕ������āA���̏��������āAfunc�Ŗ؂������牺���Ă����܂��B

## calkinwilfGetPrettier

```haskell
calkinwilfGetPrettier :: Int -> Rational
calkinwilfGetPrettier n = top $ go n
    where go n
            | mod n 2 == 0 = left $ go $ div n 2
            | otherwise    = right $ go $ div n 2
          left (Bin l _ _) = l
          right (Bin _ _ r) = r
          top (Bin _ x _) = x
```

calkinwilfGet�̉��P�łł��B���X�̔łł̓��X�g���ċA�I�ɐ������Ă����ݍ��݂�����A�Ƃ������Ƃ����Ă��܂����A�悭�l����Ɠr���Ń��X�g������K�v�͂Ȃ��āA���̂悤�ɏ����܂��B���X�g�𐶐����Ȃ�������̏������̂ق����A�������������悭�Ȃ�܂��B

��ʂɁA�W�J (unfold) ���čċA�I�ȃf�[�^����������Ə�ݍ��� (fold) ������A�Ƃ�������́A�r���̃f�[�^�����Ȃ��Ă悢���Ƃ������ł��B�r���̃f�[�^�����Ȃ��悤�Ƀv���O���������������邱�Ƃ�Z���ϊ��Ƃ����āAHaskell�ŗZ���ϊ����@�B�I�ɍs�����������낢��Ȃ���Ă��܂��B

## calkinwilfParent

```haskell
calkinwilfParent :: Rational -> Rational
calkinwilfParent x
    | x < 1 = m % (n-m)
    | x > 1 = (m-n) % n
    where m = numerator x
          n = denominator x
```

����ߓ_�̍��̎q�͕K��1��菬�����A�E�̎q�͕K��1���傫���Ƃ������Ƃ𗘗p���܂��B

## calkinwilfPrev

```haskell
calkinwilfPrev :: Rational -> Rational
calkinwilfPrev x = (m' + k * m) % m
    where m = numerator x
          n = denominator x
          div' x y = div (x-1) y
          mod' x y = mod (x-1) y + 1
          k = div' n m
          n' = mod' n m
          m' = m - n'
```

����������ߓ_�̍��̎q�ł������e�����ǂ��Ă����܂��B���̉񐔂�k�Ƃ��܂��B�����ĉE�̎q�ɂȂ�����A�e�ɍs���Ă��̍��̎q�ɍs���܂��B�����Ă܂�k��E�̎q�����ǂ�܂��B�����Ă��ǂ�����l�������ɂȂ�܂��Bk������Z�ɂ���Ē萔���Ԃŋ��߂���̂��|�C���g�ł��B

�������Ak��e�����ǂ��1/1�ɂ��ǂ���\��������܂��B���̂Ƃ��͐e��0/1�Ƃ��A���̍��̎q��0/1�Ƃ��܂��B���̉E�̎q��1/1�ƂȂ�܂��B����ŏ�肭�����̂ł��B

Calkin-Wilf�؂̍���0/1�ɂ��Ă݂܂��B����ƁA���̖؂̍��[�͂�����0/1�ɂȂ�܂��B���̖؂����Ɍ��Ă����ƁACalkin-Wilf�񂪍ŏ����牡�ɂ̂тĂ����Ă��āA���ɍs���΂����قǒ����Ȃ��Ă���̂��킩��܂��B����ɏ�ɂ�0/1�𖳌��ɐL�΂��Ă����Ă݂܂��傤�B���̗������ɖ����ł���񕪖؂����Ɍ��Ă����ƁA�Ȃ�ƁA�ǂ�������Ă�Calkin-Wilf�񂪖����ɐL�тĂ����܂��B

�������čl���Ă݂�ƁA���̃R�[�h�̈Ӗ������悭���߂Ă���͂��ł��B

## calkinwilfNext

```haskell
calkinwilfNext :: Rational -> Rational
calkinwilfNext x = n % (n' + k * n)
    where m = numerator x
          n = denominator x
          k = div m n
          m' = mod m n
          n' = n - m'
```

calkinwilfPrev�Ɠ��l�A�E�̎q�ł������e�����ǂ���(k��Ƃ��܂�)�A���̎q�ɂȂ�����e�ɍs���Ă��̍��̎q�ɍs���āAk�񍶂̎q�����ǂ�΁A�����������܂��Bk�͊���Z�ɂ���Ē萔���Ԃŋ��߂܂��B
