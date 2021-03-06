# 7 RWS 解説

## step

```haskell
import Control.Monad.Trans.RWS
import Control.Applicative
import Control.Monad

step :: RWS String String (String,Int) Int
step = do (a,n) <- get
          let (s,ss) = splitLine a
          case s of
            "name" -> ask >>= (\r -> tell $ "My name is "++r++"!\n") >> put (ss,n) >> return 1
            "sum" -> tell ("The sum is "++show n++".\n") >> put (ss,0) >> return 1
            "quit" -> tell "Goodbye!\n" >> return 0
            "error" -> tell "qawsedrftgyhujikolp\n" >> return (-1)
            s -> let m = read s in put (ss,n+m) >> tell ("I added "++show m++".\n") >> return 1

splitLine :: String -> (String,String)
splitLine s = let (a,_:b) = break (=='\n') s in (a,b)
```

ちょっと長いですが、各部分でおこなっていることは単純です。

askはモナドリーダー、tellはモナドライター、getとputはモナドステートのメンバ関数ですが、RWSはモナドリーダー・モナドライター・モナドステートの全てのインスタンスであるので、どの関数も利用できます。

## robot

```haskell
robot :: RWS String String (String,Int) ()
robot = do n <- step
           case n of
                1 -> robot
                0 -> return ()
                -1 -> tell "Oops, sorry.\n"
```

step をひたすら繰り返していくだけです。step の返り値に応じてそのまま続けるかどうか決めればよいのです。

## main

```haskell
main = do name <- getLine
          putStrLn $ "Robot "++name++" started!"
          s <- getContents
          let (_,_,output) = runRWS robot name (s,0)
          putStr output
```
