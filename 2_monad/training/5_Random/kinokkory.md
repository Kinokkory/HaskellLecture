# 5 Random ���

## calcPi

```haskell
import System.Random
import Control.Monad

calcPi :: Int -> IO Double
calcPi n = do ps <- replicateM n $ do {x<-getRand; y<-getRand; return(x,y)}
              let m = length $ filter (\(x,y) -> x*x+y*y<=1) ps
              return $ (fromIntegral m * 4.0 / fromIntegral n)

getRand :: IO Double
getRand = getStdRandom $ randomR (-1,1)
```

getRand��-1�ȏ�1�ȉ��̎����𓾂Ă��܂��B

replicateM n m �̓��i�hm��n��J��Ԃ��A����ꂽn�̌��ʂ����X�g�Ƃ��ĕԂ����i�h��\���܂��B

## main

```haskell
main = readLn >>= calcPi >>= print
```

��s�ǂ񂾌��ʂ�calcPi�ɓn���A���̌��ʂ�\�����Ă��܂��B
