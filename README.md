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

Com a triangulação feita, enviamos os triângulos e as diagonais obtidos para a função coloração(), para começarmos a colorir os vértices. Primeiro, construímos um dicionário em que as chaves são os indíces dos triângulos e os valores são as cores de cada vértice, em que 0 representa a cor azul, 1 a cor vermelho e 2 a cor verde. Atribuímos arbitrariamente essas cores nos vertíces do primeiro triângulo. Vamos para a função grafoDual(), em que criaremos o grafo dual da triangulação. Juntamos todas as diagonais em uma lista, então para criar esse grafo em que as arestas representam uma diagonal entre triângulos, basta comparar cada vértice das diagonais com cada vértice de todos os triângulos e anotá-los os dois obtidos em uma lista (A[]). Adicionamos os dois elementos de A no dicionário (que representa o grafo) nas chaves de cada triângulo obtido. Ou seja, se os triângulos 1 e 2 dividem uma diagonal então 2 vai para a chave 1 e 1 vai para a chave 2 do dicionário.

Devemos agora colorir os vértices a partir do grafo. Em buscaProfundidade(), colorimos os vértices dos triângulos que dividem a mesma diagonal com as mesmas cores e, para o outro vértice, usamos a cor restante. Fazemos isso para todos os triângulos pelo algoritmo de busca em profundidade no grafo dual que obtivemos. 

Após isso, utilizamos algumas outras estruturas e laços para plotar o polígono, com a triangulação e coloração finalizadas, e descobrir qual cor aparece menos nos vértices para, assim, conseguir uma solução para o problema.

3. Análise de Complexidade de Tempo:

Temos três algoritmos do código que influenciam mais em sua complexidade de tempo. Vamos definir que n é o número de vértices do polígono. Já é conhecido que o algoritmo de Ear Clipping possui complexidade de tempo O(n^2). Para a coloração, temos a criação do grafo dual e o algoritmo da Busca em Profundidade. Os dois laços da contrução do grafo possuem tamanhos n - 3 (npúmero de diagonais) e n - 2 (número de triângulos), necessitando assim de tempo O(n^2). É sabido também que a Busca em Profundidade possui complexidade O(n).
Dessa forma, o algoritmo do problema possui complexidade de tempo O(n^2).

4. Casos teste e entrada/saída:

Testes disponibilizados (correção no polígono points2 em que o vértice (0,0) deve aparecer apenas uma vez) + polígono = (0,0), (10,7), (12,3), (20,8), (13,17), (10, 12), (12, 14), (14,9), (8,10), (6,14), (10,15), (7,17), (0,16), (1,13), (3,15), (5,8), (-2,9), (5,5).

A entrada são os vértices do polígono no formato lista em que cada ponto é uma tupla (x,y). É bom notar que existe uma aresta entre dois vértices sse eles são vizinhos na lista. Para a saída teremos o polígono plotada com coloração e triangulação, além dos vértices em que as câmeras devem ser instaladas.
