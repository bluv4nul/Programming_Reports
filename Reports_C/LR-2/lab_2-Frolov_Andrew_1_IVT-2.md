 Указатели, арифметика указателей
### Фролов Андрей, 1 курс, ИВТ-2
___
#### Задача 1
Внутри функции int main(void) { /*...*/ } определите указатель double *** pointer = NULL;. Инициализируйте этот указатель адресом другого указателя типа double ** , который указывает на переменную double * , которая указывает на double. Используйте pointer для записи и чтения значения 2.0 в сегмент оперативной памяти для double.
##### Список идентификаторов:

| Имя    | Тип         | Смысл                                 |
| ------ | ----------- | ------------------------------------- |
| `p₃`   | `double***` | Тройной указатель (базовый уровень)   |
| `p₂`   | `double**`  | Указатель на указатель (2 уровень)    |
| `p₁`   | `double*`   | Указатель на значение (1 уровень)     |
| `p₀`   | `double`    | Конечное значение в памяти            |
| `M`    | `operator`  | Оператор выделения памяти (`malloc`)  |
| `F`    | `operator`  | Оператор освобождения памяти (`free`) |
| `Heap` | `space`     | Область динамической памяти           |
| `NULL` | `const`     | Нулевой указатель                     |

##### Код программы:
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
	*( *( *( pointer = malloc(sizeof(double**)) ) = malloc(sizeof(double *)) ) = malloc(sizeof(double)) ) = 2.0;
    printf("%.3lf\n", ***pointer);
    
    free(**pointer);
    free(*pointer);
    free(pointer);
    
    return 0;
}
```

##### Результат работы:
![](1.png)
___
#### Задача 2
Напишите программу, которая складывает два числа с использованием указателей на эти числа.
##### Математическая модель:
$$
*res = *a + *b
$$
##### Список идентификаторов:

| Имя  | Тип | Смысл                  |
| ---- | --- | ---------------------- |
| *res | int | указатель на результат |
| *a   | int | указатель на а         |
| *b   | int | указатель на б         |

##### Код программы:
```cpp
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>
#include <math.h>

int main(void)
{
    int *a = (int *)malloc(sizeof(int));
    int *b = (int *)malloc(sizeof(int));
    int *res = (int *)malloc(sizeof(int));
    SetConsoleOutputCP(CP_UTF8);
    printf("Введите первое число: ");
    scanf("%d", a);
    printf("Введите второе число: ");
    scanf("%d", b);
    *res = *a + *b;
    printf("Результат: %d", *res);
    free(a);
    free(b);
    free(res);
}
```

##### Результат работы: 
![](2.png)
___
#### Задача 3
Напишите программу, которая находит максимальное число из двух чисел, используя указатели на эти числа.
##### Математическая модель:

$$
\begin{align*}
a>b\to print(a)\\
b>a\to print(b)
\end{align*}
$$

##### Список идентификаторов:

| Имя | Тип | Смысл          |
| --- | --- | -------------- |
| *a  | int | указатель на a |
| *b  | int | указатель на b |

##### Код программы:
```cpp
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);

    int *a = (int *)malloc(sizeof(int));
    int *b = (int *)malloc(sizeof(int));

    printf("Введите первое число: ");
    scanf("%d", a);
    printf("Введите второе число: ");
    scanf("%d", b);

    if (*a > *b)
    {
        printf("Максимальное - a = %d", *a);
    }
    else
    {
        printf("Максимальное - b = %d", *b);
    }
    
    free(a);
    free(b);
}
```
##### Результат работы: 
![](3.png)
___
#### Задача 4
Напишите программу, которая создаёт одномерный динамический массив из чисел с плавающей точкой двойной точности, заполняет его значениями с клавиатуры и распечатывает все элементы этого массива, используя арифметику указателей (оператор +), а не оператор доступа к элементу массива [].
##### Список идентификаторов:

| Имя  | Тип | Смысл               |
| ---- | --- | ------------------- |
| *arr | int | динамический массив |
| size | int | размер массива      |
| i    | int | Параметр цикла      |

##### Код программы:
```cpp
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);
    
    int size;
    printf("Введите размер будущего массива: ");
    scanf("%d", &size);
    printf("\n");

    double *arr = (double*)malloc(size * sizeof(double));

    for(int i = 0; i < size;i ++)
    {
        printf("Введите %d элемент массива: ", i);
        scanf("%lf", (arr+i));
    }

    printf("\nМассив: ");
    for(int i = size-1; i >= 0; i--)
    {
        printf("%.2lf ", *(arr+i));
    }
    
    free(arr);
}
```

##### Результат работы: 
![](4.png)
___
#### Задача 5
Выведите элементы динамического массива целых чисел в обратном порядке, используя указатель и операцию декремента (--).
##### Список идентификаторов:

| Имя  | Тип    | Смысл                        |
| ---- | ------ | ---------------------------- |
| size | int    | Размер массива               |
| *ptr | double | указатель на элемент массива |
| *arr | double | массив                       |
| i    | int    | параметр цикла               |

##### Код программы:
```cpp
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>


    int main(void)
    {
        SetConsoleOutputCP(CP_UTF8);
    
        int size;
        printf("Введите размер будущего массива: ");
        scanf("%d", &size);
    
        double *arr = (double*)malloc(size * sizeof(double));
    
        double *ptr = arr;
        for(int i = 0; i < size;i ++)
        {
            printf("Введите %d элемент массива: ", i);
            scanf("%lf", ptr);
            ptr++;
        }
    
        ptr = arr+size;
        printf("Массив: ");
        for(int i = 0; i < size; i++)
        {
            ptr--;
            printf("%.2lf ", *ptr);
        }
        
        free(arr);
    }
```
##### Результат работы: 
![](5.png)
___
#### Задача 6
Определите переменную целого типа int a = 1234567890; и выведите побайтово её содержимое на экран, используя указатель char *.
##### Список идентификаторов:

| Имя  | Тип  | Смысл                   |
| ---- | ---- | ----------------------- |
| a    | int  | переменная              |
| *ptr | char | указатель на переменную |
| i    | int  | параметр цикла          |

##### Код программы:
```cpp
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);

    int a = 1234567890;
    unsigned char *ptr = (unsigned char *)&a;

    printf("Побайтовый вывод переменной:\n");
    for(int i = 0; i < sizeof(a);i++)
    {
        printf("Байт%d: %02x\n",i,(unsigned char)ptr[i]);
    }
}
```
##### Результат работы: 
![](6.png)
___
#### Задача 7
Выделите память под двумерный динамический массив, используя массив указателей на строки (см. лекции), и затем корректно освободите оперативную память.
##### Список идентификаторов:

| Имя       | Тип    | Смысл            |
| --------- | ------ | ---------------- |
| **p_matix | double | двумерный массив |
| rows      | int    | кол-во рядов     |
| cols      | int    | кол-во столбцов  |

##### Код программы:
```cpp
#include <math.h>
#include <stdlib.h>
#include <stdio.h>
#include <Windows.h>

int main(void)
{
    SetConsoleOutputCP(CP_UTF8);
    int rows, cols;

    printf("Введите количество строк: ");
    scanf("%d",&rows);
    printf("Введите количество столбцов: ");
    scanf("%d",&cols);

    double **p_matrix = = (double **)malloc(rows * sizeof(double*));

    for(int i = 0; i<rows;i++){
        p_matrix[i] = (double *)malloc(cols*sizeof(double));
    }

    for(int i = 0; i < rows; i++)
    {
        free(p_matrix[i]);
    }
    
    free(p_matrix);
}
```
##### Результат работы: 
![](7.png)
