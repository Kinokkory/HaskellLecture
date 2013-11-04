# 8 Parsec A ���

## �C���|�[�g

```haskell
import Text.Parsec
import Text.Parsec.String
import Text.Parsec.Expr
import Control.Applicative ((<$>),(<*>))
```

Text.Parsec.String �ł�

```haskell
type Parser = Parsec String ()
```

�ƒ�`����Ă���̂ŁA������g�����߂����ɃC���|�[�g���Ă��܂��B

Applicative�ł� (<|>) ����`����Ă��āAParsec�� (<|>) �ƏՓ˂���̂ŁA�K�v�ȕ������C���|�[�g���Ă��܂��B

## number

```haskell
number :: Parser Double
number = do a <- many1 digit
            b <- option "" $ (:) <$> char '.' <*> many1 digit
            c <- option "" $ (:) <$> char 'e' <*> ((++) <$> option "" (string "-") <*> many1 digit)
            spaces
            return $ read $ a++b++c
```

number ���܂Ƃ��Ƀp�[�X����͖̂ʓ|�Ȃ̂� Haskell �� read �𗘗p���Ă��܂��Boption�������e�N�j�J���Ɏg���Ă���̂ŕ�����ɂ����ł����A�ʂɓ���b�ł͂Ȃ��ł��B

�󔒂̏�������ɉ񂷂Ƃ������Ƃ����ɏd�v�ł��B

## term

```haskell
term :: Parser Double
term = number
   <|> between (char '(') (char ')') expression
   <|> do string "log" >> spaces
          char '(' >> spaces
          x <- expression
          char ',' >> spaces
          y <- expression
          char ')' >> spaces
          return $ logBase x y
```

log �̏����͈ӊO�ƊȒP�ł��B

�󔒂̏�������ɉ񂷂Ƃ������Ƃ����ɏd�v�ł��B

## expression

```haskell
table = [
    [Prefix (char '+' >> spaces >> return id), Prefix (char '-' >> spaces >> return negate)],
    [Infix (char '*' >> spaces >> return (*)) AssocLeft, Infix (char '/' >> spaces >> return (/)) AssocLeft], 
    [Infix (char '+' >> spaces >> return (+)) AssocLeft, Infix (char '-' >> spaces >> return (-)) AssocLeft],
    [Infix (char '^' >> spaces >> return (**)) AssocRight]]

expression :: Parser Double
expression = spaces >> buildExpressionParser table term
```

buildExpressionParser ��������Ǝg���Ζ�肠��܂���B

�󔒂̏�������ɉ񂷂Ƃ������Ƃ����ɏd�v�ł��B���̋󔒂�expression�ŏ��߂Ĕ�΂��܂��B

## main

```haskell
main = do s <- getContents
          parseTest expression s
```

parseTest �̓p�[�T�[���f�o�b�O�p�ɓ��������߂֗̕��Ȋ֐��ł��B
