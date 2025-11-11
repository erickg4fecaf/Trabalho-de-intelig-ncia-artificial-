# Rota Inteligente: Otimização de Entregas com Algoritmos de IA

Projeto final da disciplina *Artificial Intelligence Fundamentals*, com o objetivo de desenvolver uma solução de IA para otimização de rotas de delivery.

## 1. Descrição do Problema e Objetivos

A "Sabor Express" é uma empresa local de delivery de alimentos que enfrenta grandes desafios logísticos. As rotas de entrega são definidas manualmente pelos entregadores, com base apenas em sua experiência.

Isso resulta em:
* Rotas ineficientes, especialmente em horários de pico.
* Aumento no custo de combustível.
* Atrasos nas entregas e insatisfação dos clientes.

O **objetivo** deste projeto é substituir o sistema manual por uma solução inteligente, capaz de sugerir as melhores rotas e agrupar entregas de forma eficiente, reduzindo custos e melhorando a satisfação do cliente.

## 2. Abordagem Adotada

A solução foi dividida em duas etapas principais, tratando os dois maiores desafios da empresa:

1.  **Agrupamento de Pedidos (Clustering):** Em momentos de alta demanda, não é eficiente um entregador cruzar a cidade para uma única entrega. A solução primeiro agrupa os pedidos pendentes em "zonas" geográficas. Cada zona é atribuída a um entregador.
2.  **Otimização de Rota (Pathfinding):** Após cada entregador receber sua "zona", o sistema calcula a rota mais curta e eficiente para visitar todos os pontos de entrega dessa zona, começando e terminando na base da Sabor Express.

A cidade foi modelada como um grafo, onde locais (restaurante, pontos de entrega) são os **nós** e as ruas são as **arestas**, com pesos baseados na distância.

## 3. Algoritmos Utilizados

Para implementar a abordagem descrita, foram utilizados dois algoritmos clássicos de Inteligência Artificial:

* **K-Means (Aprendizado Não Supervisionado):** Utilizado para o agrupamento de pedidos. O algoritmo recebe as coordenadas (x,y) de todos os pedidos pendentes e os agrupa em $k$ clusters, onde $k$ é o número de entregadores disponíveis. [cite_start]Isso garante que entregas próximas sejam tratadas pelo mesmo entregador [cite: 18-19, 41].

* **$A^{*}$ (A-Estrela) (Algoritmo de Busca Heurística):** Utilizado para encontrar o caminho mais curto no grafo. [cite_start]O $A^{*}$ é ideal para problemas de rota em mapas, pois ele equilibra o custo real já percorrido (distância) com uma heurística (estimativa da distância restante), permitindo encontrar a rota ótima de forma muito eficiente[cite: 19].

## 4. Diagrama do Grafo (Modelo da Solução)

O grafo que representa o mapa da Sabor Express é definido pelos arquivos `locais.csv` (para os nós e suas coordenadas) e `mapa.csv` (para as arestas e seus pesos/distâncias).


*(Instrução: Para o seu trabalho, você pode usar uma ferramenta online para desenhar o grafo com base nos seus CSVs e incluir a imagem aqui, ou usar uma biblioteca como a NetworkX em Python para gerar a imagem).*

## 5. Análise dos Resultados e Limitações

**Eficiência:** A solução proposta é vastamente superior ao método manual. O agrupamento com K-Means garante que os entregadores operem em zonas compactas, e o $A^{*}$ garante que a rota percorrida dentro dessa zona seja a mais curta possível. Isso impacta diretamente na redução de custos de combustível e no tempo de entrega.

**Limitações:**
* **Problema do Caixeiro Viajante (TSP):** A solução atual calcula a rota do ponto A -> B, depois B -> C. Ela não resolve a ordem ótima de visita (o TSP), que é um problema computacionalmente complexo. Para o número de pedidos de uma zona, a rota é boa, mas não é "perfeita".
* **Dados Estáticos:** O sistema não considera trânsito em tempo real, que seria uma melhoria futura essencial.

**Sugestões de Melhoria:**
* Integrar com uma API de tráfego (como Google Maps) para atualizar os pesos das arestas dinamicamente.
* Implementar um algoritmo heurístico (como um genético) para resolver o "Problema do Caixeiro Viajante" (TSP) dentro de cada zona, otimizando a *ordem* das entregas.

## 6. Instruções para Execução

O projeto foi desenvolvido em Python 3.

1.  Clone este repositório.
2.  Certifique-se de que os arquivos `locais.csv`, `mapa.csv`, e `pedidos.csv` estão na mesma pasta.
3.  Instale as dependências necessárias:
    ```bash
    pip install pandas scikit-learn
    ```
4.  Execute o script principal:
    ```bash
    python otimizador_rotas.py
    ```