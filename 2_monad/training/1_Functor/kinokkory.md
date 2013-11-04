# 1 Functor ���

```haskell
import Data.Function

data X a =
    A (Int -> X a)
  | B a [Either Int a]
  | C ((a -> a -> Int) -> Int)

instance Functor X where
    fmap f (A g) = A $ \n -> fmap f (g n)
    fmap f (B x xs) = B (f x) (map (fmap f) xs)
    fmap f (C g) = C $ \h -> g (h`on`f)
```

�܂��^�ɒ��ӂ��邱�Ƃ��d�v�ł��B�������^�������Ă���ΕK���t�@���N�^���𖞂����킯�ł͂���܂��񂪁B

���a�E���ρE�֐��^�݂͂ȁA���������������Ă���̂ŁA���R�ɏ����΃t�@���N�^���𖞂����܂��B

���ہAghc�g���ł͋@�B�I��Functor��deriving�œ��o���邱�Ƃ��ł��܂����A���̃��J�j�Y���𗝉����邱�Ƃ͏d�v�ł��B

## A

�ċA�I�ȃf�[�^�^�̏ꍇ��fmap���ċA�I�ɂȂ�Ƃ������Ƃ��d�v�ł��B

## B

�f�[�^�^������q�ɂȂ��Ă���ꍇ��fmap������q�ɂȂ�Ƃ������Ƃ��d�v�ł��B(map�̓��X�g�ɂ�����fmap�ŁAfmap�Ə����Ă��\���܂���B�j

## C

�֐��^������q�ɂȂ��Ă���ꍇ�̏����Ɋ���邱�Ƃ��d�v�ł��B�t�@���N�^�̍쐬�ŕ��G�Ȃ̂͊֐��^�̈��������Ȃ̂ŗv���ӂł��B

�p�����i�h�͊֐�������q�ɂȂ����t�@���N�^�̍D��ł��B

```haskell
newtype ContT r m a = ContT {runContT :: (a -> m r) -> m r}
```

ContT r m ���t�@���N�^�����i�h�ɂȂ��Ă��܂��B

```haskell
instance Functor (ContT r m) where
    fmap f (ContT g) = ContT $ \h -> g (h . f)

instance Monad (ContT r m) where
    return x = ContT $ \f -> f x
    (ContT f) >>= g = ContT $ \h -> f (\a -> runContT (g a) h)
```
