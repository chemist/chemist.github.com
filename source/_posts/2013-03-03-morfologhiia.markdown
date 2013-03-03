---
layout: post
title: "Морфология"
date: 2013-03-03 16:27
comments: true
categories: Haskell 
---
Предыстория
-----------
Год назад, для одного из проектов мне понадобилась морфология, google и yandex вариантов для haskell не нашли.
Немного изучив предметную область, написал свой упрощенный вариант морфологии.

<!-- more -->
Описание
--------
Словарь взял из  [pymorphy](http://pythonhosted.org/pymorphy/), из функционала присутствует только нормализация, все остальное мне было не нужно.

Пример использования:
``` haskell 
module Main where

import Text.Morphology.Russian
import Data.Text (pack)

-- | import modules for show cyrillic in console
import Data.ByteString.Char8 (putStrLn)
import Data.Text.Encoding (encodeUtf8)
import Prelude hiding (putStrLn)

main::IO ()
main = do

-- | recreate binary file with morphology base, if you realy need this
-- |  makeMorph
-- | create morph.bin file in in data_dir 
-- | about data_dir see here  [about data_dir](http://neilmitchell.blogspot.ru/2008/02/adding-data-files-using-cabal.html)

-- | load binary file from data_dir, and return IO Morph
  normal <- normalForm

  let check = normal (pack "есть")
  mapM_ putStrLn $ map encodeUtf8 check
  let check = normal (pack "ржи")
  mapM_ putStrLn $ map encodeUtf8 check

```

В результате:
``` 
> :l Main
> main
быть
есть
есть
рожь
ржа
ржать
```
Если нормальной формы не найденно возвращается пустой список.

Результат по ссылке [russian-morphology](http://github.com/chemist/russian-morphology)

Установка как для любого cabal пакета.

Мысли вслух:
-----------
По хорошему нужно переписать используя [DAWG](http://en.wikipedia.org/wiki/Directed_acyclic_word_graph), в качестве хранилища для лемм и прочего + реализовать полный функционал.

