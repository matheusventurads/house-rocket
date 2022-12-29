# House Rocket

## Conhecendo o negócio
A House Rocket é uma empresa fictícia do ramo imobiliário que tem como principal meio de lucro a compra de casas em boas condições à preços mais baixos para revendas futuras a preços mais elevados. O objetivo deste projeto é utilizar análise de dados para maximixar o lucro obtido através das melhores oportunidades de negócio.

Aplicação web para visualização e análise descritiva dos dados disponível em [Streamlit](https://matheusventurads-house-rocket-app-dashboard-btndu7.streamlit.app/).

## 1. Questão de negócio
Encontrar as melhores oportunidades de compra de imóveis do portfólio da House Rocket pois time de negócio não consegue tomar boas decisões de compra sem analisar os dados. O portfólio é muito grande, muito tempo para fazer o trabalho manualmente.

Perguntas a serem respondidas:

  1. Quais são os imóveis que a House Rocket deveria comprar e por qual preço?
  2. Uma vez o imóvel comprado, qual o melhor momento para vendê-lo e por qual preço?
  
### 1.1. Entendendo os dados
A base de dados é referente a vendas realizadas entre Maio de 2014 e Maio de 2015 no Condado de King em Washington.

Atributo  | Definição
------------- | -------------
id  | Número de identificação único de casa imóvel
date  | Data de venda do imóvel
price | Preço de venda do imóvel
bedrooms | Número de quartos
bathrooms | Número de banheiros
sqft_living | Área interna do imóvel em pés quadrados
sqft_lot | Área do lote em pés quadrados
floors | Número de andares
waterfront| Indica se o imóvel tem vista para água
view | Índice de 0 a 4 para qualidade da vista da propriedade
condition | Índice de 1 a 5 sobre a condição do apartamento
grade | Índice de 1 a 13 que representa o nível de qualidade da construção e design
sqft_above | Espaço interno em pés quadrados que está acima do nível do solo
sqft_basement | Espaço interno em pés quadrados que está abaixo do nível do solo
yr_built | Ano de construção do imóvel
yr_renovated | Ano da última renovação do imóvel
zipcode | código postal
lat | latitude
long | longitude
sqft_living15 | Área interior em pés quadrados dos 15 imóveis vizinhos
sqft_lot15 | Área do lote em pés quadrados dos 15 imóveis vizinhos


## 2. Premissas de negócio
* 1.0 banheiro contém uma pia, um toalete, um chuveiro e uma banheira, valores flutuantes representam banheiros que não contém todos os elementos.
* A classificação da coluna view foi definida como: 0 = sem vista, 1 = regular, 2 = média, 3 = boa e 4 = excelente.
* A classificação da coluna condition foi definida como: 1 = muito ruim, 2 = ruim, 3 = média, 4 = boa, 5 = muito boa.
* A classificação da coluna grade foi definida como: 1-3 = muito baixa, 4-6 = baixa, 7 = média, 8-10 = alta, 11-13 = muito alta.
* Os valores iguais a 0 na coluna yr_renovated são casas que nunca foram reformadas.
* O imóvel com 33 quartos foi considerado um erro de digitação e removido do dataset.
* Localização e condição do imóvel são os principais fatores na valorização e desvalorização dos imóveis, sendo características decisivas na escolha de imóveis.
* A sazonalidade tem grande impacto no mercado imobiliário, onde as estações mais quentes apresentam maiores preços.
    
## 3. Planejamento da solução
O planejamento foi dividido em três etapas:
### 3.1. Produto Final
* Tabela com os imóveis a serem comprados.
* Tabela com os valores dos imóveis para venda.
* Aplicativo em nuvem com análise explanatória dos dados (plataforma Streamlit).

### 3.2. Ferramentas
* Python 3.10
* Pycharm
* Jupyter Notebook
* Streamlit
* Heroku

### 3.3. Processo
Para responder as perguntas de negócio, após a coleta dos dados, foi realizado o processamento e transformação, limpezas necessárias e análise explanatória.

#### 1. Quais são os imóveis que a House Rocket deveria comprar e por qual preço?
Como a localização e condição são um grandes fatores no preço, os imóveis foram agrupados por código postal e determinada a mediana de cada grupo para encontrar os preços intermediários. Logo os imóveis com valores abaixo da mediana regional foram pré-selecionados e filtrados aqueles com boas condições ou superior (>=4).

#### 2. Uma vez o imóvel comprado, qual o melhor momento para vendê-lo e por qual preço?
Considerando a impotância da sazonalidade os imóveis recomendados foram reagrupados por zipcode e estação do ano e uma nova mediana foi determinada. Em seguida as seguintes condições são aplicadas:

  1. Se o preço de compra for **maior** que a mediana regional com sazonalidade: o preço de venda é *10%* acima do valor de compra.
  2. Se o preço de compra for **menor** que a mediana regional com sazonalidade: o preço de venda é *30%* acima do valor de compra.

## 4. Os 10 principais insights dos dados
  * **H1: Imóveis que possuem vista para água, são 30% mais caros, na média.**
    
    Verdadeiro. Imóveis com vista para água são em média 212.64% mais caros.
    
  * **H2: Imóveis com data de construção menor que 1955, são 50% mais baratos, na média.**

    Falso. Imóveis construídos após 1955 são em média 0.79% mais caros.
    
  * **H3: Imóveis sem porão possuem lote 50% maior do que com porão.**

    Falso. Imóveis sem porão são em média 22.56% mais caros.
    
  * **H4: O crescimento do preço dos imóveis Y0Y (Year over Year) é de 10%.**

    Falso. O crescimento do preço YOY é de 0.52%.
    
  * **H5: Imóveis com 3 banheiros tem um crescimento MoM (Month over Month) de 15%.**

    Falso. A média do crescimento MoM é de 0.22%.
    
  * **H6: Imóveis com 3 quartos tem um crescimento MoM (Month over Month) de 15%.**

    Falso. A média de crescimento MoM é de 0.06%.
    
  * **H7: Imóveis com qualidade de construção acima da média são 20% mais caros, na média.**

    Verdadeiro. Imóveis com qualidade de construção acima da média são 93% mais caros na média.
    
  * **H8: Imóveis com vista boa ou excelente são 30% mais caros, na média.**

    Verdadeiro. Imóveis com vista boa ou excelente são em média 125% mais caros.
    
  * **H9: Imóveis renovados são 10% mais caros do que os sem reforma.**

    Verdadeiro. Imóveis renovados são em média 0.43% mais caros.
    
  * **H10: Imóveis com porão são 10% mais caros, na média.**

    Verdadeiro. Imóveis com porão são em média 27% mais caros.
  
## 5. Resultados financeiros para o negócio
Através das estratégias desenvolvidas neste projeto, obtém-se um lucro médio por imóvel de US$ 71.700,00.

E para facilitar o acesso a informação, com o desenvolvimento do [Dashboard](https://matheusventurads-house-rocket-app-dashboard-btndu7.streamlit.app/) os stakeholders podem acompanhar e definir parâmetros para encontrar novos Insights.

## 6. Conclusão e próximos passos
O projeto foi capaz de responder as perguntas de negócio definidas, com boas indicações no setor considerando o modelo de negócio da empresa. Assim como possíveis insights através das hipotéses analisadas. Contudo, há oportunidades de melhoria que podem ser refinadas em ciclos futuros, sendo:

* Incluir os insights gerados nas hipóteses nas métricas utilizadas para compra e venda dos imóveis.
* Analisar os atributos que mais influenciam no preço através de Modelos de Regressão Linear.
* Aplicar modelos de Machine Learning para prever o preço dos imóveis.
