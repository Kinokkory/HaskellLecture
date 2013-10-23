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
main = print 0
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
-- �����񂩂琮�����ЂƂǂݍ��݁A���̐����Ǝc��̕�����Ƃ̃y�A��Just�t���ŕԂ�
-- �����̓ǂݍ��݂Ɏ��s�����ꍇ��Nothing

tail :: ByteString -> ByteString
-- �����񂩂�ꕶ���ڂ����������̂�Ԃ�
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

�����ɂ������āA�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
nub :: Eq a => [a] -> [a]
-- �d������菜��

sort :: Ord a => [a] -> [a]
-- �����Ƀ\�[�g����
```

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

* ����*n* ����s���͂����ƁA�����\������x��n�𑫂��B
* "sum" �ƈ�s���͂����ƁA"the sum is *x*" �ƈ�s�\�����Ax��0�Ƀ��Z�b�g����B
* "end" �ƈ�s���͂����ƁA"goodbye" �ƈ�s�\�����I������B

�����ɂ������āA�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
lines :: String -> [String]
-- ��������s���Ƃɕ�������
```

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

�����ɂ������ẮASystem.Random���C���|�[�g���A�K�v�Ȃ�Ύ��� (�����ꂩ��) �֐�����������B

```haskell
fromIntegral :: (Integral a, Num b) => a -> b

realToFrac :: (Real a, Fractional b) => a -> b
```

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

getSubFolder path��path�Ŏw�肳�ꂽ�t�H���_�ɂ���T�u�t�H���_����񋓂���B�����������񋓂��邾���ł͎₵���̂ŕW���o�͂� searching *path* �ƈ�s�o�͂���B

getNSubFolder n path��path�Ŏw�肳�ꂽ�t�H���_����n��T�u�t�H���_�����ǂ�����ɂ���t�H���_��񋓂���BgetNSubFolder 1��getSubFolder�ɓ������B�����������񋓂��邾���ł͎₵���̂ŁA�t�H���_�������邲�ƂɕW���o�͂� I found it *n* levels down! �ƈ�s�o�͂���B

�����ɂ������ẮAControl.Monad.Trans.List��System.Directory���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
lift :: (MonadTrans t, Monad m) => m a -> t m a
-- ���i�h�������グ��

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
          n <- readLn
          l <- runListT $ getNSubfolders path n
          print l
```

# 7 RWS

RWS���i�h���������Ď��̓�̊֐�����������B

```haskell
step :: RWS String String (String,Int) Int
```

step�̓��{�b�g�̈�i�K��\���B���͕��������s��������A��s�����o�͂���B

RWS String String (String,Int) Int �̂����A

* Reader��String�̓��{�b�g�̖��O��\���B
* Writer��String�̓��{�b�g�̏o�͂�\���B
* State��(String,Int)�͓��͕�����Ɠ����̐�����\���B
* �Ԃ�l��Int�͎��̃R�[�h��\���B1�͖��I���A0�͐���I���A-1�̓G���[�ɂ��I����\���B

���͕�����

* "name" �������� "My name is *name*!" �Əo�͂��R�[�h1��Ԃ��B
* "sum" �������� "The sum is *n*." �Ɠ����̐������o�͂��A�����̐�����0�Ƀ��Z�b�g���A�R�[�h1��Ԃ��B
* "quit" �������� "Goodbye!" �Əo�͂��R�[�h0�ŏI������B
* "error" �������� "qawsedrftgyhujikolp" �Əo�͂��R�[�h-1�ŏI������B
* ���� "*m*" �������� "I added *m*." �Əo�͂��A�����̐�����m�𑫂��A�R�[�h1��Ԃ��B

```haskell
robot :: RWS String String (String,Int) ()
```

robot�̓��{�b�g��\���B

robot��step���R�[�h0��-1��Ԃ��܂�step���J��Ԃ��Â���Bstep���R�[�h-1��Ԃ����� Oops, sorry. �Əo�͂���B

�����ɂ������ẮAControl.Monad.Trans.RWS���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
ask :: MonadReader r m => m r
-- ���̎擾

tell :: MonadWriter w m => w -> m ()
-- ���O�ւ̒ǉ�

get :: MonadState s m => m s
-- ��Ԃ̎擾

put :: MonadState s m => s -> m ()
-- ��Ԃ̐ݒ�
```

## �ЂȂ���

```haskell
import Control.Monad.Trans.RWS
step :: RWS String String (String,Int) Int
{- edit here -}
robot :: RWS String String (String,Int) ()
{- edit here -}
main = do name <- getLine
          putStrLn $ "Robot "++name++" started!"
          s <- getContents
          let (_,_,output) = runRWS robot name (s,0)
          putStr output
```

# 8 Parsec A

�����̃p�[�T�[�������B

* 1234.56 �� 1.23456e3 �̂悤�ȕ���������������B�����ł�read�Ȃǂ𗘗p���Ă悢�B
* ���u���Z�q�Ƃ��� +, -, *, /, ^ (���E���E��E���E�p��) ������B
* �O�u���Z�q�Ƃ��� +, - ������B
* �O�u���Z�q��+��-���D��x���ō��ŁA*��/���D��x����Ԗڂō������A���u���Z�q��+��-���D��x���O�Ԗڂō������A^���D��x���l�ԖڂŉE�����ł���B
* ������֐��Ƃ��� log ������Blog(3,9)�Ƃ����悤�Ȍ`�Ŏg���� (���̏ꍇ�̒l��2�ł���)�B
* () �Ŏ����܂Ƃ߂���B

�ȏ�̏����𖞂����悤�ɁA���̊֐�����������B

```haskell
number :: Parser Double
expression :: Parser Double
```

�����ɂ������ẮA Text.Parsec��Text.Parsec.String��Text.Parsec.Expr���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
(<|>) :: (ParsecT s u m a) -> (ParsecT s u m a) -> (ParsecT s u m a)
(<?>) :: (ParsecT s u m a) -> String -> (ParsecT s u m a)

try :: ParsecT s u m a -> ParsecT s u m a
notFollowedBy :: (Stream s m t, Show a) => ParsecT s u m a -> ParsecT s u m ()

many, many1 :: Stream s m t => ParsecT s u m a -> ParsecT s u m [a]
between :: Stream s m t => ParsecT s u m open -> ParsecT s u m close -> ParsecT s u m a -> ParsecT s u m a
option :: Stream s m t => a -> ParsecT s u m a -> ParsecT s u m a

char :: Stream s m Char => Char -> ParsecT s u m Char
string :: Stream s m Char => String -> ParsecT s u m String
oneOf, noneOf :: Stream s m Char => [Char] -> ParsecT s u m Char
letter, digit, alphaNum, space, anyChar :: Stream s m Char => ParsecT s u m Char

buildExpressionParser :: Stream s m t => OperatorTable s u m a -> ParsecT s u m a -> ParsecT s u m a
```

�Ȃ��A�f�[�^�^�̒�`�͈ȉ��̂Ƃ���ł���B

```haskell
data Assoc = AssocNone
           | AssocLeft
           | AssocRight
-- AssocNone���������AAssocLeft���������AAssocRight���E����

data Operator s u m a = Infix (ParsecT s u m (a -> a -> a)) Assoc
                      | Prefix (ParsecT s u m (a -> a))
                      | Postfix (ParsecT s u m (a -> a))
-- Infix�����u���Z�q�APrefix���O�u���Z�q�APostfix����u���Z�q

type OperatorTable s u m a = [[Operator s u m a]]
-- �D��x���������ɉ��Z�q�������Ă���
```

## �ЂȂ���

```haskell
import Text.Parsec
import Text.Parsec.String
import Text.Parsec.Expr

number :: Parser Double
{- edit here -}

expression :: Parser Double
{- edit here -}

main = do s <- getContents
          parseTest expression s
```

# 9 Parsec B

XML�̃p�[�T�[�������B

```haskell
type Name = String
type Text = String
data Attribute = Attribute Name Text
  deriving (Show,Read)
data Contents =
    Element Name [Attribute] [Contents]
  | Text Text
  deriving (Show,Read)
```

�ȏ�̃f�[�^�^���������āA���̊֐�����������B

```haskell
name :: Parser Name
quotedText :: Parser Text
attribute :: Parser Attribute
text :: Parser Contents
element :: Parser Contents
contents :: Parser Contents
xml :: Parser Contents
```

* name �͗v�f�⑮���̖��O�ł���B
* quotedText �͑����̓��e�ƂȂ���p���Ɉ͂܂ꂽ������ł���B
* attribute �͑����ł���B
* text �͗v�f�̒��g�ƂȂ镶����ł���B
* element �͗v�f�ł���B
* contents �͗v�f�̒��g�ƂȂ�v�f���邢�͕�����ł���B
* xml �� XML���̂ł���B

���又����XML�錾��DTD�Ȃǂׂ̍��������͖������Ă��悢�B

�����ɂ������ẮA Text.Parsec��Text.Parsec.String���C���|�[�g���A�K�v�Ȃ�Ύ��̊֐�����������B

```haskell
(<|>) :: (ParsecT s u m a) -> (ParsecT s u m a) -> (ParsecT s u m a)
(<?>) :: (ParsecT s u m a) -> String -> (ParsecT s u m a)

try :: ParsecT s u m a -> ParsecT s u m a
notFollowedBy :: (Stream s m t, Show a) => ParsecT s u m a -> ParsecT s u m ()

many, many1 :: Stream s m t => ParsecT s u m a -> ParsecT s u m [a]
between :: Stream s m t => ParsecT s u m open -> ParsecT s u m close -> ParsecT s u m a -> ParsecT s u m a
option :: Stream s m t => a -> ParsecT s u m a -> ParsecT s u m a

char :: Stream s m Char => Char -> ParsecT s u m Char
string :: Stream s m Char => String -> ParsecT s u m String
oneOf, noneOf :: Stream s m Char => [Char] -> ParsecT s u m Char
letter, digit, alphaNum, space, anyChar :: Stream s m Char => ParsecT s u m Char
```

## �ЂȂ���

```haskell
import Text.Parsec
import Text.Parsec.String

type Name = String
type Text = String
data Attribute = Attribute Name Text
  deriving (Show,Read)
data Contents =
    Element Name [Attribute] [Contents]
  | Text Text
  deriving (Show,Read)

name :: Parser Name
{- edit here -}
quotedText :: Parser Text
{- edit here -}
attribute :: Parser Attribute
{- edit here -}
text :: Parser Contents
{- edit here -}
element :: Parser Contents
{- edit here -}
contents :: Parser Contents
{- edit here -}
xml :: Parser Contents
{- edit here -}
main = do s <- getContents
          parseTest xml s
```
