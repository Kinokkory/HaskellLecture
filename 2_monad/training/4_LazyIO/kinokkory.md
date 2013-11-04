# 4 Lazy IO ���

## machine

```haskell
machine :: String -> String
machine = machine' 0 . lines
machine' n (s:ss) = case s of
    "end" -> "goodbye\n"
    "sum" -> "the sum is "++show n++"\n"++machine' 0 ss
    _ -> machine' (n+read s) ss
```

��ɕ������ lines �ɂ���čs���Ƃɕ������Ă���Amachine' �ɓn���Ă��܂��B
�܂��A�����̐����������߂ɁAmachine' �Ɉ����Ƃ��� n ���������Ă��܂��B

## main

```haskell
main = interact machine
```
