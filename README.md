# Algoritmos2TP1
Problema da Galeria de Arte

TP1 - Algoritmos 2

Arthur Mota

Universidade Federal de Minas Gerais (UFMG)

1. Modelagem Computacional:

Neste trabalho, devemos solucionar o problema da galeria de arte, no qual, dada uma "planta baixa" da galeria, devemos encontrar as posições ideais das câmeras de seguranças que vão garantir a segurança do local. O formato da planta será um polígono simples não necessariamente convexo. Uma simples solução seria dividir o polígono em vários triângulos, processo chamado de triângulação, e resolvermos o problema de 3 colorção do grafo dual de cada triângulo. A cor que estiver presente em menos vértices será a escolhida para as câmeras. Para a triângulação, usaremos o algoritmo de Ear Clipping, que possui uma complexidade de tempo ótima e, para a coloração, será usado a busca em profundidade sobe grafos como algoritmo auxiliar. Quanto ao plote dos polígonos, a biblioteca HoloViews será utilizada.

2. Implementação:

Código criado na linguagem Python, usando o Jupyter Notebook e a biblioteca HoloViews.

2.1. Estrutura de Dados:

Além das listas necessárias para o armazenamento dos vértices do polígono, triângulos e diagonais obtidos após a triângulação, vamos ter o grafo dual da triangulação, em que cada nó representa um triângulo e, caso dois triângulos compartilhem uma diagonal, então existe uma diagonal entre eles. Além disso, a estrutura dicionário foi usada para dar a cor correta a cada vértice dos triângulos pós triangulação.

2.2. Algoritmos:

Começamos enviando os vértices do polígono (entrada) para a função triangulacao(). É nela que o algoritmo de Ear Clipping será utilizado. A cada vértice do polígono serão criados vetores entre o vértice atual, o anterior e o próximo para que eles sejam avaliados quanto ao produto vetorial. Caso o valor do produto vetorial for negativo, o ângulo entre os vetores é menor que 180 graus, logo podemos considerar esse triângulo formado pelos três vértices como uma orelha. Agora, verificamos se existe um vértice dentro desse triângulo na função verticeNoTriangulo(). Para cada vértice do polígono, criamos um vetor entre esse ponto e cada ponto do triângulo analisado no momento. Usamos novamente o produto vetorial para verificar se o vértice está a esquerda de todas as arestas do triângulo. Se isso não for confirmado para todos os vértices, então o triângulo atual é uma orelha e o vértice atual deve ser removido do polígono. Além disso, uma lista com as diagonais e outra com os triângulos que formam a triangulação serão criadas.



3. Análise de Complexidade de Tempo:

Temos três algoritmos do código que influenciam mais em sua complexidade de tempo. Vamos definir que n é o número de vértices do polígono. Já é conhecido que o algoritmo de Ear Clipping possui complexidade de tempo O(n^2). Para a coloração, temos a criação do grafo dual e o algoritmo da Busca em Profundidade. Os dois laços da contrução do grafo possuem tamanhos n - 3 (npúmero de diagonais) e n - 2 (número de triângulos), necessitando assim de tempo O(n^2). É sabido também que a Busca em Profundidade possui complexidade O(n).
Dessa forma, o algoritmo do problema possui complexidade de tempo O(n^2).

4. Casos teste:

Testes disponibilizados (correção no polígono points2 em que o vértice (0,0) deve aparecer apenas uma vez) + polígono = (0,0), (10,7), (12,3), (20,8), (13,17), (10, 12), (12, 14), (14,9), (8,10), (6,14), (10,15), (7,17), (0,16), (1,13), (3,15), (5,8), (-2,9), (5,5).
