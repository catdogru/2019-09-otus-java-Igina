Статистика:

||SerialGC|ParallelGC|ConcMarkSweepGC|G1GC|
|:-:|:-:|:-:|:-:|:-:|
|total time (sec)|289|278|297|279|
|minor count|4|3|10|24|
|minor total duration (ms)|172|166|287|574|
|major count|3|37|109|2|
|major total duration (ms)|941|7418|52977|254|
|list size|796354|789319|778055|810325|

**CMS**: Из-за минимизаций пауз STW инициировал сборки мусора чаще, чем другие сборщики, в результате чего общее время обработки запросов (время работы приложения к количеству добавленныъх элементов) является максимальным.

**ParallelGC**: По сравнению с CMS в лист добавлено большее количество элементов за меньшее общее время работы приложения, т.к. ParallelGC в режиме STW занимался только сборкой мусора в несколько потоков.

Лучшие результаты показал **G1**: До OOM в лист было добавлено максимальное количество элементов, суммарное время на сборки мусора оказалось минимальным. Эффективно чистил мусор в молодом поколении (24 минорные сборки), всего два раза запускалась полная (мажорная) сборка мусора.
