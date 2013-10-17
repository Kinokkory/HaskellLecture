# 1 Functor

���̃f�[�^�^�����Functor�̃C���X�^���X�ɂ���B

�܂��AX Int�^�̃f�[�^������B

```haskell
data X a =
    A (Int -> (Int,a))
  | B [(a, Maybe a)]
  | C ((a -> Int) -> Int)
```

## �ЂȂ���

```haskell
data X a =
    A (Int -> (Int,a))
  | B [(a, Maybe a)]
  | C ((a -> Int) -> Int)
{- edit here -}
x :: X Int
{- edit here -}
main = print "OK"
```

# 2 Maybe Monad

���̊֐�����������B

```haskell
readInts :: Int -> ByteString -> Maybe [Int]
```

readInts k s �́A������s�ɋ󔒋�؂�ŏ�����Ă��鐮����k�ǂݍ��݁A�����̃��X�g��Just�t���ŕԂ��B

k�����������������Ȃ��ꍇ�ANothing��Ԃ��B

Data.ByteString.Char8 ���C���|�[�g���āA
```haskell
readInt :: ByteString -> Maybe (Int,ByteString)
```
��p���Ď�������B

## �ЂȂ���

	```haskell
	import qualified Data.ByteString.Char8 as BS
	readInts :: Int -> BS.ByteString -> Maybe [Int]
	{- edit here -}
	main = do k <- readLn
          s <- BS.getContents
          print $ readInts k s

# 3 List Monad

	```haskell
	dice :: [Int] -> Int -> Int -> [Int]

dice [a1,...,ak] g n �́A�����낭�ŁAa1,...,ak��k�̖ڂ������ꂽ����������An��U�������Ƃɂ���\���̂���}�X���A�d���Ȃ������ɗ񋓂��郊�X�g��Ԃ��B

�ŏ��R�}��0�̃}�X�ɂ���B

x�̃}�X�ɂ���Ƃ���a�̖ڂ��o��΁Ax+a�̃}�X�Ɉړ�����B

������x+a��g�ȏ�Ȃ�΂����낭���S�[���������ƂɂȂ�Ag�Ɉړ����A���̌�͂�������̖ڂɂ�����炸g�ɗ��܂葱����B

�܂��Ax+a��0�����Ȃ��0�Ɉړ�����B

## �ЂȂ���

	```haskell
	import Data.List
	import Control.Monad
	dice :: [Int] -> Int -> Int -> [Int]
	{- edit here -}
	main = do g <- readLn
	          n <- readLn
	          k <- readLn
	          as <- replicateM k readLn
	          print $ dice as g n

# 4 Lazy IO

	```haskell
	machine :: String -> String

main = interact machine �Ƃ����ӂ��ɂ��Ďg���B

���̋@�B�͓����ɐ���x�������Ă���B�����l��0�ł���B

����n ����s���͂����ƁA�����\������x��n�𑫂��B

sum �ƈ�s���͂����ƁA"the sum is x" (x��x�̒l������) �ƈ�s�\�����Ax��0�Ƀ��Z�b�g����B

end �ƈ�s���͂����ƁA"goodbye" �ƈ�s�\�����I������B

## �ЂȂ���

	```haskell
	machine :: String -> String
	{- edit here -}
	main = interact machine

# 5 Random


## �ЂȂ���


# 6 


## �ЂȂ���

