|                      |       |
|----------------------|-------|
| **Time limit:**      | `2 s` |
| **Real time limit:** | `5 s` |
| **Memory limit:**    | `64M` |


### Problem sm07-4: c/data-structures/rand-heap

Вам предстоит реализовать структуру данных
[Куча](https://en.wikipedia.org/wiki/Heap_\(data_structure\)) (на максимум). Классическая реализация
на массиве слишком скучная, поэтому мы предлагаем вам кое-что новое.

Каждая вершина кучи описывается так:

    
    
    typedef struct NodeT {
        int key;
        size_t size;
        struct NodeT *left;
        struct NodeT *right;
    } NodeT;

Указатель на пустую кучу равен `NULL`. Не забывайте обрабатывать её во всех методах.

Реализуйте методы:

* `NodeT *node_new(int key)` — аллоцирует новую вершину с ключом `key`.
* `NodeT *node_merge(NodeT *v, NodeT *u)` — сливает кучу с корнем `v` с кучей с корнем `u`.
* `size_t node_size(NodeT *v)` — возвращает размер кучи с корнем `v`. Размер пустой кучи равен `0`.
* `NodeT *node_pop(NodeT *v, int *key);` — удаляет **максимальный** элемент из кучи с корнем `v`, очищает его ресурсы и возвращает указатель на новый корень. Если `key` не равен `NULL`, записывает по этому указателю значение удалённого ключа. Гарантируется, что `v` не является пустой кучей.

Аллокации разрешены только в методе `node_new`. Глобальные переменные использовать нельзя.

Ваша реализация должна работать эффективно. Подумайте над стратегией слияния куч (подсказка: 🎰).

### Examples
