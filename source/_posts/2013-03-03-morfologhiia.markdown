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

Описание
--------
Словарь взял из  [pymorphy](http://pythonhosted.org/pymorphy/), из функционала присутствует только нормализация, все остальное мне было не нужно.

Пример использования:
``` haskell 
module Main where

import Text.Morphology.Russian

-- | import modules for show cyrillic in console
import Data.ByteString (putStrLn)
import Data.Text.Encoding (encodeUtf8)

main::IO ()
main = do

--| create binary file with morphology base
  makeMorph

--| load binary file, and return IO Morph
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

