# System Programming (C++) (3 year / 2 semester)

## Exercise 1 - Операции с битами

* Вывод на экран значения целого числа в двоичной форме
* Циклический сдвиг битов
* Упаковка даты в одну четырехбайтовую переменную типа int
* Подсчет числа значащих битов

## Exercise 2 - Простейшая программа для Windows

* Освоение WinAPI GUI
* ПКМ - отображение координат курсора мыши
* ЛКМ - рисование линии
* ЛКМ + CTRL - рисование линии (веер)
* Сохранение в массив, для повторного отображения при перерисовке

## Exercise 3 - Функции WinApi для определения параметров системы

Написать программу, которая:

* определяет версию ОС ( GetVersionEx )
* определяет имя компьютера ( GetComputerName )
* определяет локальное время и часовой пояс ( GetLocalTime , GetTimeZoneInformation )
* определяет имя и язык тякущего пользователя ( GetUserDefaultLangID , VerLanguageName , GetUserName )
* текущую директорию, директорию ОС, системную директорию ( GetCurrentDirectory , GetWindowsDirectory , GetSystemDirectory )
* определят список логических дисков, их типы и свободное место на диске ( GetLogicalDrives , GetLogicalDriveString , GetDriveType , GetDiskFreeSpace )


## Exercise 4 - Низкоуровневая работа с файлами

* Программно реализовать поиск 10 файлов с расширением . txt.
* Создать на с:\ каталог FIND , внутри каталога создать файл find.dat.
* Записать в данный файл полные имена всех найденных файлов и даты создания.
* Реализовать функцию просмотра содержания файла.
* Внимание! Для выполнения всех операций с файлами и директориями используйте только функции Win 32 API.

## Exercise 5 - Программное управление реестром

Программное управление реестром
1. Написать консольное приложение, выводящие на экран хранящиеся в заданном ключе реестра переменные, их типы и значения. Имена корневого и заданного ключей вводится в программу с клавиатуры.
1. Написать консольное приложение, выводящее на экран последовательно имена всех ключей, встретившихся при поиске в реестре первой переменной с заданным именем. Имена корневого и заданного ключей вводится в программу с клавиатуры.

## Exercise 6 - Процессы в Windows

* Необходимые знания
1. Вспомнить, что запуск любого приложения автоматически приводит к созданию и запуску процесса.
1. Поучение идентификатора ID собственного процесса.
1. Запуск дочернего процесса.
1. Аргументы командной строки консольного приложения и передача через них информации в другой процесс.
1. Ожидание завершения другого процесса.

* Задание
1. Написать консольное приложение MASTER, которое должно запустить другое приложение SLAVE, после чего с помощью вызова функции Sleep в течение определенного времени ( секунд 5 – 10 ) находиться в приостановленном состоянии. Это время передается в программу MASTER через командную строку.
Имя исполнимого файла приложения SLAVE передается приложению MASTER также через командную строку. Если его нет в параметрах командной строки, то по умолчанию должен запускаться файл с именем slave.exe
1. Написать консольное приложение SLAVE, которое через командную строку получает уникальный идентификатор приложения MASTER и ждет завершения последнего, после чего завершается сам.
1. Продемонстрировать совместную работу двух приложений. Для этого на экран должна выводиться достаточно подробная информация о ходе выполнения каждого из процессов.

## Exercise 7 - Создание потоков в Win32 API для ОС MS Windows

* Составить программу для консольного процесса, который состоит из двух потоков: main и worker.

Поток main должен выполнить следующие действия:
1. Создать массив целых чисел, размерность и элементы которого вводятся с консоли.
1. Создать поток worker.
1. Найти минимальный и максимальный элементы массива и вывести их на консоль. После каждого сравнения элементов «спать» 7 миллисекунд.
1. Дождаться завершения потока worker.
1. Подсчитать количество элементов в массиве, значение которых больше среднего значения элементов массива, и вывести его на консоль.
1. Завершить работу.

Поток worker должен выполнить следующие действия:
1. Найти среднее значение элементов массива. После каждого суммирования элементов «спать» 12 миллисекунд.
1. Завершить свою работу.

* Поток worker должен найти значение суммы нечетных элементов массива. Для синхронизации потоков использовать семафор.

## Exercise 8 - Управление виртуальной памятью

* Написать консольное приложение, в котором выполняются следующие действия:
1. С помощью вызова функции *VOID GetSystemInfo( LPSYSTEM_INFO lpSystemInfo );* определяются гранулярность выделения и размер страницы виртуальной памяти;
```
typedef struct _SYSTEM_INFO
{
  WORD wProcessorArchitecture;
  WORD wReserved;
  DWORD  dwPageSize; // Размер страницы
  LPVOID lpMinimumApplicationAddress;
  LPVOID lpMaximumApplicationAddress;
  DWORD_PTR dwActiveProcessorMask;
  DWORD dwNumberOfProcessors;
  DWORD dwProcessorType;
  DWORD dwAllocationGranularity; //Гранулярность выделения
  WORD wProcessorLevel;
  WORD wProcessorRevision;
} SYSTEM_INFO;
```
1. Резервируется регион адресного пространства минимально допустимого размера и одной странице этого региона передается физическая память;
1. В начало этой страницы записываются целое число со значением 1234 и число типа double со значением 3.14, а далее за ними массив из восьми структур следующего типа: *struct MyStruct { char charVal; int intVal[ 500 ]; };* Числа и структуры в массив записывать не копированием памяти, а с помощью указателей.  
В самой первой структуре массива переменная *charVal* должна содержать код символа *‘A’*, а в каждой следующей код символа должен быть на единицу больше, чем в предыдущей. Последний элемент массива *intVal* должен содержать индекс соответствующей структуры в массиве.  
Чтобы сообразить, как записать в полученную память значения отдельных переменных или массивов, вспомните, например, как выделяется память для массива из двух целых чисел средствами языка С и как элементам этого массива присваиваются значения. Вот пример:
```
int *mas = (int*)calloc( 2, sizeof( int ) );
mas[ 0 ] = 123;
mas[ 1 ] = 456;
```
1. Одной страницы памяти недостоточно для размещения всех структур, поэтому в програме необходимо написать обработчик исключений для передачи программе очередной страницы при попытке записи в область виртуальной памяти, которой физическая память еще не передана.
1. По завершении записи каждой очередной структуры на экран надо вывести в одну строку значения индекса структуры, текущее число переданных страниц физической памяти, значения *charVal* и последнего элемента массива *intVal*, адрес начала структуры и адрес начала массива *intVal.*