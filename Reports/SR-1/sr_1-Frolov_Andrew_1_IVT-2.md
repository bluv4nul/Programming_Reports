### Фролов Андрей, 1 курс, ИВТ-2
___
#### Задача 1
**Динамический массив и вычисление среднего арифметического**
Напишите программу на языке Си, которая: 
• Запрашивает у пользователя количество элементов массива (целое число N). 
• Динамически выделяет память для массива из N элементов типа float. 
• Заполняет массив значениями, введёнными с клавиатуры. 
• Вычисляет и выводит среднее арифметическое всех элементов массива. 
• При обращении к элементам массива используйте арифметику указателей (без оператора []). 
• Освобождает выделенную память в конце работы программы.
##### Математическая модель:
$$
\begin{align*}
res = \frac{\sum_{i = 0}^{n}a(i)}{n}
\end{align*}
$$
##### Список идентификаторов:

| Имя  | Тип    | Смысл                          |
| ---- | ------ | ------------------------------ |
| n    | int    | количество элементов в массиве |
| s    | float  | переменная для результата      |
| *arr | float* | динамический массив            |
| i    | int    | параметр цикла                 |

##### Код программы:
```c
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);

    int n;
    float s;

    printf("Введите размерность массива N: ");
    scanf("%d",&n);

    float *arr = (float *)malloc(n*sizeof(float));
    
    for(int i = 0; i < n; i++)
    {
        printf("Введите %d элемент массива: ", i);
        scanf("%f", (arr+i));
    }
    
    for(int i = 0; i < n; i++)
    {
        s+=*(arr+i);
    }
    s/=n;
    printf("Среднее арифметическое: %.2f", s);
    
    free(arr);
}
```
##### Результат работы: 
![](Programming/Reports/SR-1/1.png)
#### Задача 2 
Каталог книг Создайте структуру Book, которая содержит следующие поля: 
• title – массив символов (строка) для хранения названия книги (максимум 50 символов); 
• author – массив символов для хранения имени автора (максимум 50 символов); 
• year – целое число, обозначающее год издания книги. 
Напишите программу, которая: 
• Создаёт массив из 3-х экземпляров структуры Book. 
• Запрашивает у пользователя данные для каждой книги (название, автора и год издания). 
• Выводит информацию обо всех книгах на экран, используя для этого отдельную функцию printBook(), которая принимает указатель на структуру Book. 
##### Математическая модель:
$$
\begin{align*}
Book = (title,author,year) 
\begin{cases}
title &\in строка \ название \ книги \ (до \ 50 \ символов)\\
author &\in строка \ название \ книги \ (до \ 50 \ символов)\\
year &\in \mathbb{Z}
\end{cases}

\end{align*}
$$
$$
\begin{align*}
&printBook(Book \ book) \to void \\ \\
&printBook = 
\begin{cases}
Вывести \ название \\ 
Вывести \ автора \\
Вывести \ год написания книги
\end{cases}
\end{align*}
$$
##### Список идентификаторов:

| Имя          | Тип         | Смысл           |
| ------------ | ----------- | --------------- |
| book         | struct      | Структура книги |
| title[50]    | char        | название        |
| author[50]   | char        | автор           |
| year         | int         | год             |
| printBook    | void        | функция вывода  |
| arr_books[3] | struct book | массив книг     |
| i            | int         | параметр цикла  |

##### Код программы:
```c
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

struct book
{
    char title[50];
    char author[50];
    int year;
};

void printBook(struct book *book)
{
    printf("Название книги: %s\n", book -> title);
    printf("Автор книги: %s\n", book -> author);
    printf("Год издания книги: %d\n", book -> year);
}

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);

    struct book arr_books[3];
    printf("Введите 3 книги:\n");
    printf("__________________________\n");
    for(int i = 0; i < 3; i++)
    {
        printf("Введите название %d книги: ", (i+1));
        fgets(arr_books[i].title, 50, stdin);
        printf("Введите автора %d книги: ", (i+1));
        fgets(arr_books[i].author, 50, stdin);
        printf("Введите год написания %d книги: ", (i+1));
        scanf("%d", &arr_books[i].year);
        printf("__________________________\n");
        getchar();
    }

    for(int i = 0; i < 3; i++){
        printBook(&arr_books[i]);
        printf("__________________________\n");
    }
}
```
##### Результат работы: 

![](Programming/Reports/SR-1/2.png)
#### Задача 3
Определение сезона по номеру месяца Создайте перечисление Season со следующими значениями: 
• WINTER, SPRING, SUMMER, AUTUMN Напишите программу, которая: 
• Запрашивает у пользователя номер месяца (целое число от 1 до 12). 
• На основе введённого номера месяца определяет и выводит соответствующий сезон: – Зима: декабрь (12), январь (1) и февраль (2); – Весна: март (3), апрель (4) и май (5); – Лето: июнь (6), июль (7) и август (8); – Осень: сентябрь (9), октябрь (10) и ноябрь (11). 
• Для определения сезона можно использовать условные операторы (if-else) или конструкцию switch. 
##### Математическая модель:
$$
\begin{align*}
Season = \left\{WINTER,SPRING,SUMMER,AUTUMN\right\} \to\

\begin{cases}
WINTER \ если \ (12,1,2)  \\
SPRING \ если \ (3, 4, 5)  \\
SUMMER \ если \ (6,7,8)  \\ 
WINTER \ если \ (9,10,11)  \\
\end{cases}

\end{align*}
$$
##### Список идентификаторов:

| Имя    | Тип         | Смысл                              |
| ------ | ----------- | ---------------------------------- |
| season | enum        | перечисление времен года           |
| month  | int         | месяц                              |
| season | enum season | переменная для присвоения значения |

##### Код программы:
```c
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

enum season{
    winter, autumn, summer, spring 
}; 

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);

    int month;
    printf("Введите номер месяца (1-12): ");
    scanf("%d",&month);

    enum season season;

    switch(month){
        case 12:
        case 1:
        case 2:
            season = winter;
            break;
        case 3:
        case 4:
        case 5:
            season = spring;
            break;
        case 6:
        case 7:
        case 8:
            season = summer;
            break;
        case 9:
        case 10:
        case 11:
            season = autumn;
            break;
    }

    switch (season)
    {
        case winter:
            printf("Winter");
            break;
        case summer:
            printf("Summer");
            break;
        case autumn:
            printf("Autumn");
            break;
        case spring:
            printf("Spring");
            break;
    }
    
}
```
##### Результат работы: 
![](Programming/Reports/SR-1/3.png)