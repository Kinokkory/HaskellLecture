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
   +--3
+--2
|  |     +--6
|  |  +--5
|  |  |  +--7
|  +--4
|     |     +--10
|     |  +--9
|     |  |  +--11
|     +--8
1
|  +--13
|  |  +--14
+--12
   +--15
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

calkinwilfTree �́ACalkin-Wilf�؂��̂��̂�\���B

calkinwilfSeq �́ACalkin-Wilf���\���BcalkinwilfTree�𕝗D��T�����邱�Ƃɂ���������B

calkinwilfGet n �́ACalkin-Wilf���n�Ԗڂ̐���Ԃ��B�������ACalkin-Wilf�؂����ǂ邱�Ƃɂ���� O(log n) �ŋ��߂�B

## �ЂȂ���

```haskell
import Data.Ratio
{- copy from 'binary tree' -}
calkinwilfTree :: Tree Rational
{- edit here -}
calkinwilfSeq :: [Rational]
{- edit here -}
calkinwilfGet :: Int -> Rational
{- edit here -}
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

Stern-Brocot�؂Ƃ��������[���؂�����B

![Stern-Brocot Tree](/sternbrocot.png)

���̖؂͖����񕪖؂ł���A�ߓ_�͐��̊���L�����ł���B

���̖؂̍�����������邽�߂ɁA�e�ߓ_��3�̗L�����̑g����Ȃ�ł��l����i�֋X��A1/0���L�����Ƃ��ĔF�߂Ă����j�B

���� (0/1, 1/1, 1/0) �ł���B�ߓ_ (a/b, c/d, e/f) �̍��̎q�� (a/b, (a+c)/(b+d), c/d)�A�E�̎q�� (c/d, (c+e)/(d+f), e/f)�ł���B

���̖؂̊e�ߓ_ (x,y,z) �� y �ɕς������̂�Stern-Brocot�؂ł���B

�ȏ�𓥂܂��ABinary Tree �Ŏ��������f�[�^�Ɗ֐����������āA���̊֐�����������B

```haskell
sternbrocotTree :: BinaryTree Rational
```

## �ЂȂ���

```haskell
import Data.Ratio
{- copy from 'binary tree' -}
```
