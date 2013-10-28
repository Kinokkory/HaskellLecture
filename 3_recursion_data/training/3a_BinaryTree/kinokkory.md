# 3a Binary Tree ���

## takeBinaryTree

```haskell
takeBinaryTree :: Int -> BinaryTree a -> BinaryTree a
takeBinaryTree 0 _ = Tip
takeBinaryTree n Tip = Tip
takeBinaryTree n (Bin l x r) = Bin (takeBinaryTree (n-1) l) x (takeBinaryTree (n-1) r)
```

�����ނ˃��X�g��̊֐� take :: Int -> [a] -> [a] �Ɠ����ł��B

## showBinaryTree

```haskell
showBinaryTree :: Show a => BinaryTree a -> String
showBinaryTree t = unlines $ showBinaryTree' 0 t
showBinaryTree' :: Show a => Int -> BinaryTree a -> [String]
showBinaryTree' _ Tip = []
showBinaryTree' i (Bin l x r)
    | i== 0  = sr++[sx]++sl
    | i== 1  = map ("|  "++) sr ++ ["+--"++sx] ++ map ("   "++) sl
    | i== -1 = map ("   "++) sr ++ ["+--"++sx] ++ map ("|  "++) sl
    where sl = showBinaryTree' 1 l
          sr = showBinaryTree' (-1) r
          sx = show x
```

�����񂪓񎟌��̍\���������Ă���̂ŁA�����̃��X�g�̃��X�g�i������̃��X�g�j�Ƃ��Ĉ����̂������ł��傤�B�s�̃��X�g����邩����Ƃ���̃��X�g����邩�A�Ƃ�����肪����܂����A���̖��ł͍s�̃��X�g�������������₷���Ǝv���܂��B
