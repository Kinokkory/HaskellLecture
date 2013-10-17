# 1 Functor

���̃f�[�^�^�����Functor�̃C���X�^���X�ɂ���B

```haskell
data X a =
    A (Int -> X a)
  | B a [Either Int a]
  | C ((a -> a -> Int) -> Int)
```
## �ЂȂ���

```haskell
data X a =
    A (Int -> X a)
  | B a [Either Int a]
  | C ((a -> a -> Int) -> Int)
{- edit here -}
main = print "OK"
```

# 2 Maybe Monad

���̊֐���Maybe���i�h���������Ď�������B

```haskell
readInts :: Int -> ByteString -> Maybe [Int]
```

readInts k s �́A������s�ɋ󔒋�؂�ŏ�����Ă��鐮����k�ǂݍ��݁A�����̃��X�g��Just�t���ŕԂ��B
k�����������������Ȃ��ꍇ�ANothing��Ԃ��B

�����ɂ������ẮAData.ByteString.Char8 ���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
readInt :: ByteString -> Maybe (Int,ByteString)
```

## �ЂȂ���

```haskell
import qualified Data.ByteString.Char8 as BS
readInts :: Int -> BS.ByteString -> Maybe [Int]
{- edit here -}
main = do k <- readLn
          s <- BS.getContents
          print $ readInts k s
```

# 3 List Monad

���̊֐���List���i�h���������Ď�������B

```haskell
dice :: [Int] -> Int -> Int -> [Int]
```

dice [a1,...,ak] g n �́A�����낭�ŁAa1,...,ak��k�̖ڂ������ꂽ����������An��U�������Ƃɂ���\���̂���}�X���A�d���Ȃ������ɗ񋓂��郊�X�g��Ԃ��B��������̖ڂ͕��ł���\��������B

�ŏ��R�}��0�̃}�X�ɂ���Bx�̃}�X�ɂ���Ƃ���a�̖ڂ��o��΁Ax+a�̃}�X�Ɉړ�����B������x+a��0�����Ȃ��0�Ɉړ�����B

�܂��Ax+a��g�ȏ�Ȃ�΂����낭���S�[�������̂ŁAg�Ɉړ����A���̌�͂�������̖ڂɂ�����炸g�ɗ��܂葱����B

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
```

# 4 Lazy IO

���̊֐���x���]��IO���������Ď�������B

```haskell
machine :: String -> String
```

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
```

# 5 Random

���̊֐��𗐐���IO���������Ď�������B

```haskell
calcPi :: Int -> IO Double
```

calcPi n �́A-1<=x<=1,-1<=y<=1�͈̔͂ŕ��ʏ�̓_(x,y)��n�����_���Ɏ��A�����̓_�̒��ŒP�ʉ~�ɓ����Ă�����̂̌��𐔂��邱�ƂŁA�~�����̋ߎ��l�����߂�B

## �ЂȂ���

```haskell
import System.Random
calcPi :: Int -> IO Double
{- edit here -}
main = do n <- readLn
          print <$> calcPi n
```

# 6 Monad Trans

���̊֐�����������B

```haskell
getSubFolder :: FilePath -> ListT (IO FilePath)
getNSubFolder :: FilePath -> Int -> ListT (IO FilePath)
```

getSubFolder path��path�Ŏw�肳�ꂽ�t�H���_�ɂ���T�u�t�H���_����񋓂���B
getNSubFolder n path��path�Ŏw�肳�ꂽ�t�H���_����n��T�u�t�H���_�����ǂ�����ɂ���t�H���_��񋓂���BgetNSubFolder 1��getSubFolder�ɓ������B

�����ɂ������ẮASystem.Directory���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
getDirectoryContents :: FilePath -> IO [FilePath]
-- �t�H���_���̃T�u�t�H���_�ƃt�@�C����񋓂���B
-- �Ō��".."(�e�t�H���_)��"."(�t�H���_���g)��t��������̂Œ��ӂ���B

doesDirectoryExist :: FilePath -> IO Bool
-- �p�X���t�H���_���ǂ������肷��B
```

�Ȃ��AFilePath��String�̌^�V�m�j���ł���B

## �ЂȂ���

```haskell
import Control.Monad.Trans.List
import System.Directory
getSubfolders :: FilePath -> ListT IO FilePath
{- edit here -}
getNSubfolders :: FilePath -> Int -> ListT IO FilePath
{- edit here -}
main = do path <- getLine
          n <- readLn :: IO Int
          l <- runListT $ getNSubfolders path n
          print l
```

# 7 RWS

## �ЂȂ���

# 8 Parsec A

## �ЂȂ���


# 9 Parsec B

## �ЂȂ���

# 10 Parsec C

## �ЂȂ���

