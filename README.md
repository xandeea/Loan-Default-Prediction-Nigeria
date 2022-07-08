<h1 align="center">Modelo de Predição Pagamento de Empréstimo Nigeria</h1>
Esse notebook foi desenvolvido como a última atividade de um grupo de estudos em ciência de dados. Nessa semana, a ideia era aplicar os conhecimentos adquiridos durante os meses que se passou o grupo. Para isso, deveríamos participar de uma competição da plataforma Zindi (https://zindi.africa/competitions/data-science-nigeria-challenge-1-loan-default-prediction).

## 1. Sobre a competição
A ideia da competição era prever o empréstimo pedido por algum cliente foi bom ou ruim. Para isso, foram disponibilizadas três bases de dados diferentes.

### 1.1 Base de Dados Demográfica:
A primeira delas contém informações demográficas sobre cada pessoa:

<i>(Data de Nascimento, Tipo de Conta no Banco, Latitude e Longitude, Nome do Banco, Localização do Banco, Tipo de Profissão e Nível de Escolaridade).</i>


### 1.2 Base de Dados Empréstimos Anteriores:
A segunda disponibilizava informações sobre empréstimos anteriores que a pessoa já havia realizado. Cada pessoa pode ter vários empréstimos associados a seu id, cada empréstimo também com um id diferente. As informações disponíveis eram:

<i>(Quantidade de empréstimo, Data de aprovação/criação/fechamento do empréstimo, Valor pedido de empréstimo, Quanto o cliente pagou (Valor + Taxas), Número do empréstimo que a pessoa estava pedindo, Data de quando deveria ser feito o primeiro pagamento e de quando realmente foi feito o primeiro pagamento, além da informação se o cliente havia sido indicado por outro cliente).</i>


### 1.3 Base de Dados do Empréstimo Atual:
Por fim, a última base de dados disponibilizada contém as informações do empréstimo atual:

<i>(Quantidade de empréstimo, Data de aprovação/criação/fechamento do empréstimo, Valor pedido de empréstimo, Quanto o cliente pagou (Valor + Taxas), Número do empréstimo que a pessoa estava pedindo, Prazo do empréstimo, além de um id, caso o cliente tivesse sido indicado por outro cliente).</i>


## 2. Preparação dos Dados
Antes da criação dos modelos, foram feitas algumas modificações nas variáveis disponíveis. Na tabela demográfica, as colunas de latitude e longitude foram convertidas em cidade, estado e condado. Também foi criada uma coluna de idade para ser usada ao invés de data de nascimento. 

Na tabela de empréstimos anteriores, foram criadas novas variáveis de quantos dias o cliente levou para fazer o primeiro pagamento e quantos dias levou para quitar o empréstimo. Além disso, por ser uma tabela com ids repetidos, as linhas com mesmo id foram agrupadas, retirando valores mínimo, máximo e a média de cada coluna.

Por fim, os três datasets foram concatenados e foi criada uma nova coluna contendo a informação se o cliente havia sido indicado por outro ou não.
  

## 3. Criação do Modelo
Para a criação do Pipeline, foram testados diversos tipos de imputação para valores faltantes, tanto para variáveis categóricas quanto para variáveis numéricas. Também foram testadas diferentes técnicas para transformação das variáveis categóricas em variáveis numéricas e também técnicas de reescalamento dos dados. Por fim, os modelos classificadores testados foram:
<ul>
    <li>KNeighborsClassifier</li>
    <li>SVC</li>
    <li>LogisticRegression</li>
    <li>DecisionTreeClassifier</li>
    <li>RandomForestClassifier</li>
    <li>CatBoostClassifier</li>
    <li>LGBMClassifier</li>
    <li>XGBClassifier</li>
   </ul>

### 3.1 Melhores Modelos
Para avaliação dos modelos, utilizou-se a métrica do F1-score, com validação cruzada com 5 folds. Abaixo, você consegue visualizar os 5 melhores modelos, ordenados pelo maior valor na validação cruzada.

<table border="1">       
  <tr>
    <td><b>Imputer Numérico</b></td>
    <td><b>Imputer Categórico</td>
    <td><b>Scaler</td>
    <td><b>Encoder</td>
    <td><b>Classificador</td>
    <td><b>Score F1</td>
    <td><b>Média Score com Validação Cruzada</td>
  </tr>
  <tr>
    <td>mean</td>
    <td>constant</td>
    <td>StandardScaler</td>
    <td>TargetEncoder</td>
    <td>SVC</td>
    <td>0.880245</td>
    <td>0.880197</td>
  </tr>
  <tr>
    <td>mean</td>
    <td>most_frequent</td>
    <td>StandardScaler</td>
    <td>TargetEncoder</td>
    <td>SVC</td>
    <td>0.880245</td>
    <td>0.880082</td>
  </tr>
  <tr>
    <td>median</td>
    <td>constant</td>
    <td>StandardScaler</td>
    <td>TargetEncoder</td>
    <td>SVC</td>
    <td>0.880245</td>
    <td>0.880081</td>
  </tr>
  <tr>
    <td>median</td>
    <td>constant</td>
    <td>StandardScaler</td>
    <td>LeaveOneOutEncoder</td>
    <td>LogisticRegression</td>
    <td>0.882456</td>
    <td>0.879994</td>
  </tr>
  <tr>
    <td>mean</td>
    <td>constant</td>
    <td>StandardScaler</td>
    <td>LeaveOneOutEncoder</td>
    <td>LogisticRegression</td>
    <td>0.882946</td>
    <td>0.879994</td>
  </tr>
</table>
