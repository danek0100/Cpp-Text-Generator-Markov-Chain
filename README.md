# Lab-8

## Лабораторный практикум №8 (Генератор текста)

![GitHub pull requests](https://img.shields.io/github/issues-pr/HSE-CS/tp-lab-8)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/HSE-CS/tp-lab-8)

![Relative date](https://img.shields.io/date/1616792399)

### Задание

Разработать программу-генератор текста на основе цепи Маркова. 

### Краткие сведения из теории

Мы можем синтезировать текст, используя символы, сочетания символов, слова, сочетания слов, предложения.
Одной из разновидностей синтеза является частотный синтез.

Алгоритм частотного синтеза на уровне символов прост:

```
строка S =пустое слово
пока не достигнем строки заданной длины
  из таблицы символов выбираем символ C с вероятностью P(C)
  дописываем символ C к строке S
```

В результате образуется строка заданной длины, состоящая из символов.

Полученная строка, скорее всего, совершенно бессмысленна (и трудночитаема). Повысить читаемость можно, составляя текст из k-сочетаний, наиболее часто встречающихся в языке.

Например, в русском языке, часто встречаются следующие последовательности букв

```
СТ, НО, ЕН, ТО, НА, ОВ, НИ, РА, ВО, КО
СТО, ЕНО, НОВ, ТОВ, ОВО, ОВА
```

Для получения еще более читаемого текста нужно формировать текст либо из слов, либо из сочетаний слов.

Рассмотрим пример, основанный на **цепи Маркова**

Рассматриваемый алгоритм в качестве исходных данных будет использовать специальную таблицу префиксов, состоящих из двух слов и суффиксов, представляющих собой одно слово. Эта таблица образуется в результате анализа большого текстового файла.

Алгоритм генерирует фразы на выходе, случайным образом выбирая для определенного префикса следующий за ним суффикс.

Описание алгоритма:

```
поместить в W1 и W2 первые два слова
вывести W1 и W2
цикл:
  случайно выбрать W3 из набора суффиксов
  к префиксу W1 и W2
  заменить W1 и W2 на W2 и W3
  повторить цикл
```

### Использование стандартной библиотеки С++

В данной работе должны использоваться элементы стандартной библиотеки.


```c++
typedef deque<string> prefix;          // очередь префиксов
map<prefix, vector<string> > statetab; // префикс-суффиксы
```

В качестве параметров необходимо задать размер префикса (в словах) и объем генерируемого текста:

```c++
const int NPREF=2; // количество слов в префиксе
const int MAXGEN=1000; //объем текста на выходе
```

Процесс работы программы можно представить следующим образом:

- открывается входной файл на чтение
- файл читается по словам и в памяти создается таблица префиксов и суффиксов
- после обработки входного файла начинается процесс генерации выходного текста
- из таблицы берется первый префикс и случайно выбирается для него продолжение (в вифе суффикса)
- происходит переход на очередной префикс и для него снова выбирается суффикс
- генерация заканчивается либо при достижении заданного размера, либо при обработке последнего префикса

### Пример работы


Пример генерации текста на основе текста ''Сказка о Золотой рыбке''

```
Жил старик со своею старухой У самого синего моря; 
Они жили в ветхой землянке Ровно тридцать лет и три года. 
Старик ловил неводом рыбу, Старуха пряла свою пряжу. 
Раз он в море синее просилась, Дорогою ценою откупалась: 
Откупалась чем только пожелаю Не посмел я взять с неё корыто, 
Наше-то совсем раскололось". Отвечает золотая рыбка: 
"Не печалься, ступай себе с богом". Воротился старик ко старухе, 
Что ж он видит? Высокий терем. На крыльце стоит его старуха 
В дорогой собольей душегрейке, Парчевая на маковке кичка, 
Жемчуги огрузили шею, На руках золотые перстни, На ногах красные сапожки. 
Перед нею усердные слуги; Она бьёт их, за чупрун таскает. 
Говорит старик своей старухе: "Здравствуй, барыня-сударыня дворянка! 
Чай, теперь твоя душенька довольна". На него прикрикнула старуха, 
На конюшне служить его послала. Вот неделя, другая проходит, 
Ещё пуще старуха бранится, Не даёт старику мне покою: 
Надобно ей новое корыто; Наше-то совсем раскололось". 
Отвечает золотая рыбка: "Не печалься, ступай себе с богом! 
Добро! будет старуха царицей!" Старичок к старухе воротился 
Глядь: опять перед ним землянка; На пороге сидит его старуха, 
А пред нею разбитое корыто. корыто. 
```

## Тестирование

В данном проекте необходимо реализовать следующие тесты:

- формирование префикса из заданного числа слов
- формирование записи "префикс-суффикс"
- выбор единственного суффикса из вектора суффиксом (использование ПСЧ)
- выбор суффикса из вектора, содержащего несколько вариантом (ПСЧ)
- формирование текста заданной длины (на основе таблицы, заполненной вручную)


## Состав проекта

- **include/textgen.h**
- **src/textgen.cpp**
- **src/main.cpp**
- **test/tests.cpp**

## Список участников/веток

1. Малинин  Дмитрий Дмитриевич  19 ПМИ-2 b60
1. Бакланов Алексей Александрович   19 ПМИ-2 b61
1. Баринов  Даниил  Сергеевич   19 ПМИ-1 b62
1. Богомазов    Михаил  Васильевич  19 ПМИ-1 b63
1. Бугров   Лев Валерьевич  19 ПМИ-1 b64
1. Бузанов  Егор    Андреевич   19 ПМИ-1 b65
1. Варлачёв Валерий Максимович  19 ПМИ-1 b66
1. Голованов    Денис   Максимович  19 ПМИ-1 b67
1. Дробот   Елизавета   Денисовна   19 ПМИ-1 b68
1. Жаравина Полина  Дмитриевна  19 ПМИ-1 b69
1. Зайцев   Тимур   Олегович    19 ПМИ-1 b70
1. Кабанов  Денис   Сергеевич   19 ПМИ-1 b71
1. Канев    Владислав   Олегович    19 ПМИ-1 b72
1. Карцева  Мария   Дмитриевна  19 ПМИ-1 b73
1. Касьянов Никита  Юрьевич 19 ПМИ-1 b74
1. Козлова  Дарья   Андреевна   19 ПМИ-1 b75
1. Кузнецов Михаил  Дмитриевич  19 ПМИ-1 b76
1. Лавров   Артём   Романович   19 ПМИ-1 b77
1. Матвеев  Андрей  Сергеевич   19 ПМИ-1 b78
1. Машанова Карина  Алексеевна  19 ПМИ-1 b79
1. Наумов   Никита  Александрович   19 ПМИ-1 b80
1. Нещеткин Глеб    Максимович  19 ПМИ-1 b81
1. Пасманик Ирина   Дмитриевна  19 ПМИ-1 b82
1. Рогозян  Анастасия   Тимофеевна  19 ПМИ-1 b83
1. Соболев  Данил   Александрович   19 ПМИ-1 b84
1. Софронов Валерий Александрович   19 ПМИ-1 b85
1. Трутнев  Алексей Игоревич    19 ПМИ-1 b86
1. Тумаков  Вадим   Сергеевич   19 ПМИ-1 b87
1. Фролова  Ольга   Михайловна  19 ПМИ-1 b88
1. Шарибжанова  Диана   Рашидовна   19 ПМИ-1 b89
1. Щеникова Анна    Юрьевна 19 ПМИ-1 b90
1. Андросов Вадим   Дмитриевич  19 ПМИ-2 b91
1. Бирина   Елизавета   Сергеевна   19 ПМИ-2 b92
1. Булатов  Дмитрий Александрович   19 ПМИ-2 b93
1. Демашов  Никита  Александрович   19 ПМИ-2 b94
1. Добряев  Иван    Александрович   19 ПМИ-2 b95
1. Дрожжачих    Евгений Валерьевич  19 ПМИ-2 b96
1. Егорова  Кристина    Олеговна    19 ПМИ-2 b97
1. Загоскин Владислав   Андреевич   19 ПМИ-2 b98
1. Зарубина Ирина   Михайловна  19 ПМИ-2 b99
1. Иванов   Даниил  Андреевич   19 ПМИ-2 b100
1. Клыков   Антон   Романович   19 ПМИ-2 b101
1. Королев  Денис   Витальевич  19 ПМИ-2 b102
1. Краюшкина    Екатерина   Алексеевна  19 ПМИ-2 b103
1. Назаров  Вячеслав    Андреевич   19 ПМИ-2 b104
1. Оленев   Дмитрий Сергеевич   19 ПМИ-2 b105
1. Панина   Полина  Сергеевна   19 ПМИ-2 b106
1. Прыгаев  Денис   Алексеевич  19 ПМИ-2 b107
1. Рогов    Андрей  Дмитриевич  19 ПМИ-2 b108
1. Симонова Арина   Валерьевна  19 ПМИ-2 b109
1. Созинов  Кирилл  Игоревич    19 ПМИ-2 b110
1. Титова   Нина    Ивановна    19 ПМИ-2 b111
1. Уртюков  Илья    Алексеевич  19 ПМИ-2 b112
1. Хорев    Егор    Алексеевич  19 ПМИ-2 b113
1. Шабаршин Леонид  Георгиевич  19 ПМИ-2 b114

## Алгоритм выполнения работы

Для выполнения работы необходимо:

1. Выполнить *fork* репозитария в свой аккаунт.
1. Выполнить клонирование репозитария из своего аккаунта к себе на локальную машину (`git clone`).
1. Создать ветку **git** с индивидуальным номером (`git branch имя_ветки`).
1. Сделать ветку активной (`git checkout имя`).
1. Необходимо разместить как исходные файлы с решениями задач, поместив **cpp** файлы в **src**, а заголовочные - в **include**. 
1. Добавить файлы в хранилище (`git add`).
1. Выполнить фиксацию изменений (`git commit -m "комментарий"`).
1. Отправить содержимое ветки в свой удаленный репозитарий (`git push origin имя_ветки`).
1. Создать пул-запрос в репозитарий группы и ждать результата от **Travis-CI**.

