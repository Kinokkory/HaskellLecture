# Maybe Monad ���

## readInts

```haskell
import qualified Data.ByteString.Char8 as BS

readInts :: Int -> BS.ByteString -> Maybe [Int]
readInts 0 _ = return []
readInts k s = do (n,s') <- BS.readInt s
                  ns <- readInts (k-1) (BS.tail s')
                  return (n:ns)
```

�ċA����Ƃ���������Maybe���i�h�̊�{�I�Ȏg������������Ώ\���ł��B

## main

```haskell
main = do k <- readLn
          s <- BS.getContents
          print $ readInts k s
```

BS.getContents �œ��͑S�̂�ǂݍ���ł��܂��B��ʂɁA���͈͂�C�ɑS���ǂݍ���ŕ�����Ƃ��ď������Ă����ق����A�������ǂݍ��ނ��������������ł��B
