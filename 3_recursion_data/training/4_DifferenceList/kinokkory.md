## Difference List ���

## flatten

```haskell
flatten :: BinaryTree a -> [a]
flatten t = flatten' t []
flatten' :: BinaryTree a -> ([a] -> [a])
flatten' Tip = id
flatten' (Bin l x r) = flatten' l . ([x]++) . flatten' r
```

���̃\�[�X�R�[�h�͔��ɃV���v���ł����A�ǂ������v���Z�X�ŏ��������̂Ȃ̂����ڂ��������Ă����܂��B

�^�C�g���� Difference List �Ƃ����̂́A���{�ꂾ�ƍ������X�g�Ƃ����āA���X�g�����X�g�̍����Ƃ��ĕ\������f�[�^�^�̂��Ƃł��B�^�Ƃ��ẮA

```haskell
type DiffList a = [a] -> [a]
```

�ƂȂ��Ă��āA���X�g�ƍ������X�g�͈ȉ��̂悤�ɑ��ݕϊ��ł��܂��B

```haskell
list2difflist :: [a] -> DiffList a
list2difflist l = (l++)

difflist2list :: DiffList a -> [a]
difflist2list d = d []
```

���X�g�ƍ������X�g�ł́A�����ɂ�����������ς��܂��B

```haskell
(++) :: [a] -> [a] -> [a]
[] ++ b = b
(a:as) ++ b = a : (as++b)

(++*) :: DiffList a -> DiffList a -> DiffList a
a ++* b = a . b
```

�������Ă݂܂��傤�B

```haskell
aas = replicate 100000 [0]

go 1 = foldr (++) [] aas
go 2 = foldl (++) [] aas
go 3 = difflist2list $ foldr (++*) id $ map list2difflist aas
go 4 = difflist2list $ foldl (++*) id $ map list2difflist aas

main = do n <- readLn
          print $ length $ go n
```

�������Ă݂�ƁAgo 1 �� go 3 �� go 4 �͌����������ł����Ago 2 �͑�ώ��Ԃ�������܂��B(++) �͉E�����ň�Ԍ�������������ǂ��A(++*) �͉E�����ł��������ł������͕ς��Ȃ��̂ł��B(++*) �� (.) �Ɠ������A���� f . (g . h) �� (f . g) . h �͂܂����������ł���̂ŁA���R�̂��Ƃł��B

������������ł��傤���A�𓚂̃\�[�X�R�[�h�́A++*�𗘗p�������̂ł��B���̂悤�ɏ����������Ƃ��ł��܂��B

```haskell
type DiffList a = [a] -> [a]

list2difflist :: [a] -> DiffList a
list2difflist l = (l++)

difflist2list :: DiffList a -> [a]
difflist2list d = d []

(++*) :: DiffList a -> DiffList a -> DiffList a
a ++* b = a . b

flatten :: BinaryTree a -> [a]
flatten = difflist2list . flatten'
flatten' :: BinaryTree a -> DiffList a
flatten' Tip = list2difflist []
flatten' (Bin l x r) = flatten' l ++* list2difflist [x] ++* flatten' r
```
