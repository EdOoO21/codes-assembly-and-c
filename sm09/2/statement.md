|                      |       |
|----------------------|-------|
| **Time limit:**      | `1 s` |
| **Real time limit:** | `5 s` |
| **Memory limit:**    | `64M` |


### Problem sm09-2: unix/files/writechar-2

Опишите структуру `FileWriteState` для хранения состояния буферизованного вывода в файл. Структура
может быть описана примерно так:

    
    
    struct FileWriteState
    {
        int fd;              // "файловый дескриптор", для вывода на стандартный поток вывода - 1
        unsigned char *buf;  // указатель на буфер
        ssize_t bufsize;     // размер буфера
        // здесь потребуется добавить поля для реализации буферизованной записи
    };

Определите глобальную переменную:

    
    
    struct FileWriteState *stout;

В вашей реализации переменная `stout` должна быть уже инициализирована корректным указателем на
корректную структуру состояния записи при запуске программы (то есть используйте инициализацию
глобальных переменных). Буфер должен быть выделен статически, его размер должен быть равен 4KiB.

Напишите подпрограммы `writechar` и `flush` для буферизированного посимвольного вывода.

    
    
    void writechar(int c, struct FileWriteState *out);
    void flush(struct FileWriteState *out);

Функция `writechar` принимает байт для вывода в параметре `c`, а в параметре `out` — указатель на
структуру состояния вывода. Этот байт не отправляется на поток вывода с помощью системного вызова
write немедленно, а накапливается в буфере вывода. Когда буфер вывода заполняется, вызывается
подпрограмма `flush` для записи содержимого буфера на устройство.

Функция `flush` принимает один парамер — указатель на структуру состояния вывода. Функция использует
системный вызов `write` для записи содержимого буфера за один раз. Будем предполагать, что операция
записи завершается успешно и полностью записывает буфер. Размер буфера - 4KiB.

Решение будет компилироваться без стандартной библиотеки (точка входа - `_start`). Используйте
[ассемблерную вставку](https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html) для совершения
системного вызова write.

Подсказка для тестирования: программа, использующая `writechar`, должна не забыть вызвать `flush`
перед завершением, так как в противном случае будет потеряна часть данных, еще находящаяся в
выходном буфере.

