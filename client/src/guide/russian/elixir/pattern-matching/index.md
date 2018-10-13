---
title: Pattern Matching
localeTitle: Соответствие шаблону
---
## Соответствие шаблону

Сравнение шаблонов - это метод, который Эликсир наследует от Erlang. Это очень мощный метод, который позволяет нам извлекать более простые подструктуры из сложных структур данных, таких как списки, кортежи, карты и т. Д.

Матч состоит из двух основных частей: левой и правой. Правая сторона - это структура данных любого рода. Левая сторона пытается сопоставить структуру данных с правой стороны и привязать любые переменные слева к соответствующей субструктуре справа. Если совпадение не найдено, оператор вызывает ошибку.

Простейшим совпадением является одиночная переменная слева и любая структура данных справа. Эта переменная будет соответствовать любому. Например:  
`x = 12`  
`x = "Hello"`  
`IO.puts(x)`

Вы можете размещать переменные внутри структуры, чтобы вы могли захватить подструктуру. Например:  
`[var_1, _unused_var, var_2] = [{"First variable"}, 25, "Second variable" ]`  
`IO.puts(var_1)`  
`IO.puts(var_2)`

Это сохранит значения, `{"First variable"}` в var _1 и `"Second variable"` в var_ 2. Существует также специальная \_ переменная (или переменные с префиксом «\_»), которая работает точно так же, как и другие переменные, но сообщает elixir, «Удостоверьтесь, что что-то здесь, но мне все равно, что это такое». В предыдущем примере \_unused\_var была одной такой переменной.

Используя эту технику, мы можем сопоставить более сложные шаблоны. Например, если вы хотите развернуть и получить номер в кортеже, который находится внутри списка, который сам находится в списке, вы можете использовать следующую команду:  
`[_, [_, {a}]] = ["Random string", [:an_atom, {24}]]`  
`IO.puts(a)`

Вышеупомянутая программа генерирует следующий результат:  
`24`

Это будет привязывать к 24. Другие значения игнорируются, поскольку мы используем '\_'.

При сопоставлении с образцом, если мы используем переменную справа, ее значение используется. Если вы хотите использовать значение переменной слева, вам нужно использовать оператор вывода.

Например, если у вас есть переменная «a», имеющая значение 25, и вы хотите сопоставить ее с другой переменной «b», имеющей значение 25, тогда вам нужно ввести -  
`a = 25`  
`b = 25`  
`^a = b`

Последняя строка соответствует текущему значению a вместо присвоения ему значению b. Если у нас есть несоответствующий набор левой и правой стороны, оператор сопоставления вызывает ошибку. Например, если мы попытаемся сопоставить кортеж со списком или списком размера 2 со списком размера 3, будет отображаться ошибка.