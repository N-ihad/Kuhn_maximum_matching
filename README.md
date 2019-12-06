# Kuhn Maximum Matching Algorithm
### Алгоритм Куна для поиска максимального паросочетания
![](https://sun9-68.userapi.com/c205724/v205724869/30ac/jJ-m0lpX1i4.jpg)

## Описание реализации алгоритма на C++
'n1' - количество вершин первого множества двудольного графа  
'n2' - количество вершин второго множества двудольного графа
generateBipartiteGraph(n1, n2) - функция "случайной" генерации ребер между двумя множествами двудольного графа. На выходе двумерный массив.
bipartiteGraph[i] - список ребер из вершины 'x' первого множества (список номеров вершин, в которые ведут эти рёбра из 'x'). Вершины занумерованы следующим образом:  
Из первого множества: 1, 2, ... n1  
Из второго множества: 1, 2, ... n2  

Массив 'match' содержит информацию о текущем паросочетании в графе. Для удобство эта информация взята для второго множества вершин, то есть match[i] - номер вершины первой доли, связанной ребром с вершиной 'i' второй доли (или -1, если никакого ребра паросочетания из 'i' не выходит).  
Массив 'usedVertices' - массив посещённостей вершин в обходе в глубину, чтобы не заходить в одну вершину дважды.

Функция kuhnAlgorithm - обход в глубину. Возвращает значение 'true', если удалось найти увеличивающую цепь из вершины 'x', при этом считается, что эта функция уже произвела чередование паросочетания вдоль найденной цепи. Внутри функции просматриваются все рёбра, исходящие из вершины 'x' первой доли, и затем проверяется: если это ребро ведёт в ненасыщенную вершину 'to', либо если эта вершина 'to' насыщена, но удаётся найти увеличивающую цепь рекурсивным запуском из match[to], то увеличивающая цепь - найдена, и перед возвратом из функции с результатом 'true' произвходим чередование в текущем ребре: перенаправляем ребро, смежное с 'to', в вершину 'x'.

В начале программы текущее паросочетание считается пустым, список 'match' заполяется числами -1. Затем перебирается вершина 'x' первого множества, и из неё запускается обход в глубину kuhnAlgorithm, предварительно обнулив массив 'usedVertices'.

Максимальное паросочетание будет содержаться в массиве 'match'.
