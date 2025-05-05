# Projeto de Visualização de Dados de E-commerce

Este repositório contém o código Python utilizado para a visualização de dados de um conjunto de dados de e-commerce, carregado do arquivo `ecommerce_preparados.csv`. O objetivo é explorar e apresentar insights relevantes sobre os dados através de diferentes tipos de gráficos gerados com as bibliotecas `matplotlib.pyplot` e `seaborn`.

## Conjunto de Dados

O conjunto de dados `ecommerce_preparados.csv` contém informações sobre produtos de e-commerce, incluindo detalhes como gênero, marca, preço, quantidade vendida, notas (reviews), número de avaliações e frequência da marca.

## Pré-processamento dos Dados

Antes da visualização, os seguintes passos de pré-processamento foram realizados:

* **Remoção de Colunas:** As colunas 'Desconto', 'Material', 'Temporada', 'Review1', 'Review2', 'Review3', 'Desconto\_MinMax', 'Marca\_Cod', 'Material\_Cod', 'Temporada\_Cod' e 'Material\_Freq' foram removidas para focar em colunas relevantes para a análise de visualização.
* **Tratamento de Valores Nulos:** Valores nulos e strings vazias foram preenchidos com 0.
* **Cálculo da Frequência de Gênero:** A frequência percentual de cada gênero foi calculada e armazenada na coluna 'genero\_freq'.
* **Filtragem de Gêneros Raros:** Gêneros com menos de 5% de ocorrência foram excluídos do DataFrame para focar em categorias mais representativas.
* **Formatação de Texto:** As colunas 'Gênero' (removendo espaços e convertendo para maiúsculas) e 'Marca' (capitalizando cada palavra) foram formatadas para melhor consistência.
* **Salvamento do DataFrame Processado:** O DataFrame resultante foi salvo em um novo arquivo `Ecommerce_analise.csv`.

## Gráficos Gerados

Os seguintes gráficos foram criados para analisar o conjunto de dados processado:

1.  **Produtos por Gênero (Gráfico de Barras):**
    * Visualiza a frequência de produtos por gênero após o pré-processamento.
    * Utiliza um gráfico de barras com a cor roxa para representar cada gênero e sua respectiva frequência.
    * Os eixos são rotulados como 'Gênero' e 'Frequência'.
    * A coluna numérica 'gen\_int' foi criada como uma representação numérica da coluna 'Gênero'.

2.  **Distribuição de Vendas por Gênero (Boxplot):**
    * Compara a distribuição da quantidade de itens vendidos ('Qtd\_Vendidos\_Cod') entre diferentes gêneros.
    * Utiliza um boxplot do `seaborn` para mostrar a mediana, quartis e outliers da quantidade vendida para cada gênero.
    * O eixo y ('Qtd Vendidos') está em escala logarítmica para melhor visualização da dispersão dos dados.
    * Os rótulos do eixo x ('Gênero') foram rotacionados para melhor leitura.

3.  **Top 10 Marcas (Gráfico de Pizza):**
    * Exibe as 10 marcas mais frequentes no conjunto de dados em um gráfico de pizza, mostrando a proporção de cada marca em relação ao total das 10.
    * As fatias são rotuladas com o nome da marca e a porcentagem de frequência, com tamanho de fonte ajustado.

4.  **Correlação (Mapa de Calor):**
    * Visualiza a matriz de correlação entre as colunas 'Qtd\_Vendidos\_Cod', 'Preço', 'gen\_int', 'N\_Avaliações' e 'Marca\_Freq'.
    * Utiliza um mapa de calor da biblioteca `seaborn` com anotações dos valores de correlação e um mapa de cores 'coolwarm', com tamanho das anotações ajustado.
    * Os rótulos dos eixos x foram rotacionados para melhor leitura.

5.  **Regressão Avaliações e Notas (Gráfico de Dispersão com Regressão):**
    * Analisa a relação entre a nota do produto ('Nota') e o número de avaliações ('N\_Avaliações').
    * Utiliza um gráfico de dispersão com uma linha de regressão ajustada aos dados, gerado pela função `regplot` do `seaborn`.
    * Os pontos do gráfico têm uma certa transparência (`alpha`) e cores específicas.

6.  **Moda de Preços (Gráfico de Densidade KDE):**
    * Visualiza a distribuição de probabilidade do preço dos produtos através de um gráfico de densidade kernel (KDE) do `seaborn`.
    * A área sob a curva é preenchida com a cor roxa.

7.  **Frequência de Notas (Histograma):**
    * Exibe a distribuição da frequência das notas dos produtos.
    * Utiliza um histograma com 100 bins e cor roxa, com transparência ajustada. Uma grade é sobreposta para facilitar a leitura.

8.  **Preço vs. Frequência da Marca (Gráfico de Dispersão):**
    * Explora a relação entre o preço dos produtos ('Preço') e a frequência da marca ('Marca\_Freq').
    * Utiliza um gráfico de dispersão para visualizar se marcas com maior frequência têm alguma tendência em relação ao preço de seus produtos.

## Bibliotecas Utilizadas

* `pandas` (como `pd`): Para manipulação e análise de dados, incluindo leitura do arquivo CSV e criação de DataFrames.
* `seaborn` (como `sns`): Para a criação de gráficos estatísticos como boxplot, mapa de calor, regressão e gráfico de densidade.
* `matplotlib.pyplot` (como `plt`): Para a criação de gráficos básicos como barras, pizza, histograma e para personalizações gerais dos gráficos.
