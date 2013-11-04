# 6 Monad Trans ���

## getSubfolders

```haskell
getSubfolders :: FilePath -> ListT IO FilePath
getSubfolders path = ListT $ getDirectoryContents path >>= return . map ((path++"/")++) . filter (\p -> p/=".."&&p/=".") >>= filterM doesDirectoryExist
```

ListT �Ƃ����f�[�^�\�z�q���������Ƃ��d�v�ł��B

## getNSubfolders

```haskell
getNSubfolders :: FilePath -> Int -> ListT IO FilePath
getNSubfolders path 0 = return path
getNSubfolders path n = do p <- getNSubfolders path (n-1)
                           q <- getSubfolders p
                           lift (putStrLn $ "I found it "++show n++" levels down!")
                           return q
```

���Ƃ� getSubfolders ���������ă��X�g���i�h�Ɠ��l�ɍs���܂��B
lift �� IO �������グ���邱�Ƃ��d�v�ł��B

## main

```haskell
main = do path <- getLine
          n <- readLn
          l <- runListT $ getNSubfolders path n
          print l
```

������ runListT ���������Ă��܂��B
