# Cognitivo.AI_AirbnbRJ
Análise exploratória dos Preços praticados pelo Airbnb no Rio de Janeiro. Fonte:http://insideairbnb.com/get-the-data.html

### *Perguntas do Teste Cognitivo AI*

a. Como foi a definição da sua estratégia de modelagem?

b. Como foi definida a função de custo utilizada?

c. Qual foi o critério utilizado na seleção do modelo final?

d. Qual foi o critério utilizado para validação do modelo?
Por que escolheu utilizar este método?

e. Quais evidências você possui de que seu modelo é
suficientemente bom?

### Respostas:
**a.** A estratégia baseou-se no preço, assim foram eliminados os atributos cuja corelação com o preço é baixa, permitindo assim a escolha de um modelo que melhor refletisse a colinearidade dos dados.

**b.** Foi definida como o Erro Médio Quadrático. Essa função é a que queremos minimizar é o que chamamos de função custo ou função objetivo e normalmente é representada pela letra L (de “loss”, em inglês). Por exemplo, no caso de regressão linear, a função custo que queremos minimizar era erro quadrático médio: L=(y−y^)².

**c.** O modelo final foi definido com base na melhor acuracidade possível para a análise em estudo. Assim o modelo que apresentou melhor acuracidade foi o Modelo de Floresta Randômica com o menor erro médio quadrático e score mais assertivo.

**d.** O critério de validação foi definido com base nos parâmetros cross-validados para reafirmar a acuracidade do modelo escolhido. Como dito acima, a escolha se deu por apresentar maior acurácia e menor erro médio.

**e.** Após ajustar e instanciar os hiperparâmetros do modelo, minimizou-se um pouco mais o erro médio quadrático, reforçando a ideia intuitiva da relação direta do preço com a quantidade de noites de estadia associada à localização da unidade para aluguel no AIRBnB


## Estudos Preliminares:
### Porque fazer Seleção de Features?

*   Algumas Features (Features não informativas) pode adicionar ruído ao modelo.
    * Exemplo: *nome, id, id_de_variaveis*
*   Modelos simples são explicativos, devemos evitar a perda da explicabilidade dos nossos modelos.
*   Muitas features podem causar problemas como tempos excessivos para treino, ou ainda dificuldades de colocar modelos em produção.
### Tipos de Algoritmos e Métodos

*   **Filter Methods** : Métodos de seleção que utiliza medidas estatísticas para atribuir um score para cada feature. As features são classificadas pelo score para serem mantidas ou removidas do modelo. Normalmente se usam testes univariados que consideram a independência da feature com a variável alvo. Exemplo: chi squared, scores com coeficiente de correlação.

*   **Wrapper Methods** : Métodos de seleção que selecionam um conjunto de features, onde diferentes combinações são preparadas, avaliadas e comparadas. Um modelo preditivo é usado para avaliar a combinação de features a atribuir um score baseado em uma acurácia de modelo. Exemplo: algoritmo RFE 



*   **Embedded Methods** : Métodos Embedded aprendem quais feature melhor contribuiem para a acurácia do modelo no momento de construção do modelo. Exemplo: métodos de penalização, algoritmos Lasso, Elastic NEt e Ridge Regression.

**Erro Quadrático Médio**

Em regressão temos um problema da forma  y^=y+ϵ em que y é a variável que queremos prever e y^ é nossa estimativa dessa variável. Agora, nós queremos prever y a partir de variáveis independentes XX. Por simplicidade, vamos supor apenas uma variável independente. Então, podemos reescrever o problema como y^=f(x)+ϵ  em que f(x) é a função que mapeia x em y e que queremos estimar. Ainda além, nós vamos assumir que ϵ tem média zero e é variância σ2. Dessa forma, podemos dizer que a probabilidade conjunta de y e x é dada por

P(x,y)=P(y|x)P(x) em que P(y|x) é a probabilidade de y dado x, que segue uma distribuição tal que P(y|x)∼N(y^,σ2). Com isso, podemos provar que minimizar o erro quadrático médio gera uma estimativa y^ que é um estimador de máxima verossimilhança para y. A prova é um pouco complicada e não é essencial para nosso propósito aqui. De qualquer forma, deixo aqui o link dela. Basicamente, o que fazemos é usar o fato da função distribuição de probabilidade seguir uma gaussiana e então mostra-se que maximizar a probabilidade dessa gaussiana é equivalente a minimizar o erro quadrático médio, definido como

L=(yy−w^w^X)T(yy−w^w^X)
O que é importante perceber é que minimizar o erro quadrático médio fará com que y^ será o estimador de máxima verossimilhança para y, ou seja, y^ será a média condicional de y, E[x|y]. Como assumimos que y tem uma distribuição gaussiana quando condicionado em x, isso que dizer que podemos representar nossas previsão como uma reta que passa pelo ponto de maior probabilidade dessa distribuição gaussiana condicional

**Erro Absoluto Médio** 

Em vez de mirar nossa estimativa na média condicional, podemos mirá-la na mediana condicional. Para tanto, basta trocar a função objetivo de 1m∑ϵ2 para
L=1m∑∥ϵ∥
Isto é, trocamos a minimização do erro quadrático médio para a minimização do erro absoluto médio.
