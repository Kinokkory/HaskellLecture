# 1a Binary Tree

```haskell
data BinaryTree a = Bin (BinaryTree a) a (BinaryTree a) | Tip
```

���̓񕪖؂ɂ��āA���̊֐�����������B

```haskell
takeBinaryTree :: Int -> BinaryTree a -> BinaryTree a
showBinaryTree :: Show a => BinaryTree a -> String
```

takeBinaryTree n t �� t ��������[�� n �܂Ő؂������񕪖؂�\���B���̐[����1�Ƃ���B

showBinaryTree t �� t �𕶎���ɕϊ�����B
���Ƃ��Ύ��̂悤�Ȃ��Ƃł���B

```
> putStrLn $ showBinaryTree $ Bin (Bin (Bin Tip 3 Tip) 2 (Bin (Bin (Bin Tip 6 Tip) 5 (Bin Tip 7 Tip)) 4 (Bin (Bin (Bin Tip 10 Tip) 9 (Bin Tip 11 Tip)) 8 Tip))) 1 (Bin (Bin Tip 13 (Bin Tip 14 Tip)) 12 (Bin Tip 15 Tip))
   +--15
+--12
|  |  +--14
|  +--13
1
|     +--8
|     |  |  +--11
|     |  +--9
|     |     +--10
|  +--4
|  |  |  +--7
|  |  +--5
|  |     +--6
+--2
   +--3
```

## �ЂȂ���

```haskell
data BinaryTree a = Bin (BinaryTree a) a (BinaryTree a) | Tip

instance Show a => Show (BinaryTree a) where
  show = showBinaryTree

takeBinaryTree :: Int -> BinaryTree a -> BinaryTree a
{- edit here -}

showBinaryTree :: Show a => BinaryTree a -> String
{- edit here -}

main = print $ takeBinaryTree 4 $ Bin (Bin (Bin Tip 3 Tip) 2 (Bin (Bin (Bin Tip 6 Tip) 5 (Bin Tip 7 Tip)) 4 (Bin (Bin (Bin Tip 10 Tip) 9 (Bin Tip 11 Tip)) 8 Tip))) 1 (Bin (Bin Tip 13 (Bin Tip 14 Tip)) 12 (Bin Tip 15 Tip))
```

# 1b Calkin-Wilf

Calkin-Wilf�؂Ƃ��������[���؂�����B

![Calkin-Wilf Tree](/calkinwilf.png)

���̖؂͖����񕪖؂ł���A�ߓ_�͐��̊���L�����ł���B

����1/1�ł���A�ߓ_ m/n �̍��̎q�� m/(m+n) �ŉE�̎q�� (m+n)/n �ł���B

Calkin-Wilf�؂𕝗D��T�����邱�Ƃɂ���ē�����L������

```
1/1, 1/2, 2/1, 1/3, 3/2, 2/3, 3/1, 1/4, 4/3, 3/5, 5/2, 2/5, 5/3, 3/4, 4/1, ...
```

��Calkin-Wilf��Ƃ����A���܂��܂ȋ����ׂ������������Ă���B���ׂĂ̐��̊���L���������ꂼ���x���������B�܂��An�Ԗڂ̗L�����̕����n+1�Ԗڂ̗L�����̕��q�Ɠ������B

�ȏ�𓥂܂��ABinary Tree �Ŏ��������f�[�^�Ɗ֐����������āA���̊֐�����������B

```haskell
calkinwilfTree :: BinaryTree Rational
calkinwilfSeq :: [Rational]
calkinwilfGet :: Int -> Rational
```

calkinwilfTree �́ACalkin-Wilf�؂��̂��̂ł���B

calkinwilfSeq �́ACalkin-Wilf��ł���BcalkinwilfTree�𕝗D��T�����邱�Ƃɂ���������B

calkinwilfGet n �́ACalkin-Wilf���n�Ԗڂ̐���Ԃ��B1�Ԗڂ�1/1�ł���BCalkin-Wilf�؂����ǂ邱�Ƃɂ���� O(log n) �ŋ��߂�B

�����ɂ������ẮAData.Ratio���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
(%) :: Integral a => a -> a -> Ratio a
-- �L����������
numerator :: Integral a => Ratio a -> a
-- ���q�����߂�
denominator :: Integral a => Ratio a -> a
-- ��������߂�
```

�Ȃ��ARational��Ratio Integer�̌^�V�m�j���ł���B

## �ЂȂ���

```haskell
import Data.Ratio

{- copy from 'binary tree' -}

calkinwilfTree :: BinaryTree Rational
{- edit here -}

calkinwilfSeq :: [Rational]
{- edit here -}

calkinwilfGet :: Int -> Rational
{- edit here -}

main = print $ takeBinaryTree 5 calkinwilfTree
-- main = print $ take 100 $ calkinwilfSeq
-- main = print $ calkinwilfGet 100
```

## ���܂�

���̊֐������ꂼ��萔���Ԃœ��삳���邱�Ƃ��ł���B����������Ύ��������݂�B

```haskell
calkinwilfParent :: Rational -> Rational
-- Calkin-Wilf�؏�ŁA�e�ɂȂ�L����

calkinwilfPrev :: Rational -> Rational
-- Calkin-Wilf��ɂ����āA��O�ɂȂ�L����

calkinwilfNext :: Rational -> Rational
-- Calkin-Wilf��ɂ����āA���ɂȂ�L����
```

# 1c Stern-Brocot

Stern-Brocot�؂Ƃ�������܂������[���؂�����B

![Stern-Brocot Tree](/sternbrocot.png)

���̖؂͖����񕪖؂ł���A�ߓ_�͐��̊���L�����ł���B

���̖؂̍�����������邽�߂ɁA�܂��e�ߓ_��3�̐��̊���L�����̑g����Ȃ�؂����i�����ł̂݁A1/0���L�����Ƃ��ĔF�߂�j�B���� (0/1, 1/1, 1/0) �Ƃ��A�ߓ_ (a/b, c/d, e/f) �̍��̎q�� (a/b, (a+c)/(b+d), c/d)�A�E�̎q�� (c/d, (c+e)/(d+f), e/f) �Ƃ���B�������ďo���オ���������񕪖؂̊e�ߓ_ (x,y,z) �� y �ɕς������̂��AStern-Brocot�؂ł���B

���̖؂͂��܂��܂ȋ����ׂ������������Ă���B���ׂĂ̐��̊���L���������ꂼ���x���������B�܂��A�}�̍ŉ����̂悤�ɁA�����珇�ɐߓ_����ׂ�ƁA���ꂢ�ɏ����ɕ��ԁB

�ȏ�𓥂܂��ABinary Tree �Ŏ��������f�[�^�Ɗ֐����������āA���̊֐�����������B

```haskell
sternbrocotTree :: BinaryTree Rational
simplest :: (Double,Double) -> Rational
rationals :: Integer -> [Rational]
```

sternbrocotTree ��Stern-Brocot�؂��̂��̂ł���B

silplest (x,y) �� x�ȏ�y�ȉ��̗L�����̂����A����ƕ��q�̘a���ŏ��̂��̂����߂�B���Ȃ݂ɁA���̂Ƃ���������q�����ꂼ��ŏ��ƂȂ�BsternbrocotTree�����܂������Ď�������B

rationals k �͕���ƕ��q�̘a��k�ȉ��̐��̊���L�����������ɗ񋓂���BsternbrocotTree�����܂������Ď�������B

�����ɂ������ẮAData.Ratio���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
(%) :: Integral a => a -> a -> Ratio a
-- �L����������
numerator :: Integral a => Ratio a -> a
-- ���q�����߂�
denominator :: Integral a => Ratio a -> a
-- ��������߂�
```

�Ȃ��ARational��Ratio Integer�̌^�V�m�j���ł���B�܂��A1 % 0�Ƃ������̓G���[�ɂȂ�̂ŁA�H�v���Ď�������B

## �ЂȂ���

```haskell
import Data.Ratio

{- copy from 'binary tree' -}

sternbrocotTree :: BinaryTree Rational
{- edit here -}

simplest :: (Double,Double) -> Rational
{- edit here -}

rationals :: Integer -> [Rational]
{- edit here -}

main = print $ takeBinaryTree 5 sternbrocotTree
-- main = print $ simplest (3.14,3.15)
-- main = print $ rationals 20
```
