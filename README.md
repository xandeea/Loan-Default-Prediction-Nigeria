<h1 align="center">Modelo de Predição Pagamento de Empréstimo Nigeria</h1>
<p align="left">Esse notebook foi desenvolvido como a última atividade de um grupo de estudos em ciência de dados. Nessa semana, a ideia era aplicar os conhecimentos adquiridos durante os meses que se passou o grupo. Para isso, deveríamos participar de uma promoção da plataforma Zindi (https://zindi.africa/competitions/data-science-nigeria-challenge-1-loan-default-prediction).</p>

## 1. Sobre a competição
<p align="left">A ideia da competição era prever o empréstimo pedido por algum cliente foi bom ou ruim. Para isso, foram disponibilizadas três bases de dados diferentes.

### 1.1 Base de Dados Demográfica:
A primeira delas contém informações demográficas sobre cada pessoa:

<i>(Data de Nascimento, Tipo de Conta no Banco, Latitude e Longitude, Nome do Banco, Localização do Banco, Tipo de Profissão e Nível de Escolaridade).</i>
</p>

### 1.2 Base de Dados Empréstimos Anteriores:
A segunda disponibilizava informações sobre empréstimos anteriores que a pessoa já havia realizado. Cada pessoa pode ter vários empréstimos associados a seu id, cada empréstimo também com um id diferente. As informações disponíveis eram:

<i>(Quantidade de empréstimo, Data de aprovação/criação/fechamento do empréstimo, Valor pedido de empréstimo, Quanto o cliente pagou (Valor + Taxas), Número do empréstimo que a pessoa estava pedindo, Data de quando deveria ser feito o primeiro pagamento e de quando realmente foi feito o primeiro pagamento, além da informação se o cliente havia sido indicado por outro cliente).</i>
</p>

### 1.3 Base de Dados do Empréstimo Atual:
Por fim, a última base de dados disponibilizada contém as informações do empréstimo atual:

<i>(Quantidade de empréstimo, Data de aprovação/criação/fechamento do empréstimo, Valor pedido de empréstimo, Quanto o cliente pagou (Valor + Taxas), Número do empréstimo que a pessoa estava pedindo, Prazo do empréstimo, além de um id, caso o cliente tivesse sido indicado por outro cliente).</i>
</p>

## 2. Preparação dos Dados
<p align="left">Antes da criação dos modelos, foram feitas algumas modificações nas variáveis disponíveis. Na tabela demográfica, as colunas de latitude e longitude foram convertidas em cidade, estado e condado. Também foi criada uma coluna de idade para ser usada ao invés de data de nascimento. 

Na tabela de empréstimos anteriores, foram criadas novas variáveis de quantos dias o cliente levou para fazer o primeiro pagamento e quantos dias levou para quitar o empréstimo. Além disso, por ser uma tabela com ids repetidos, as linhas com mesmo id foram agrupadas, retirando valores mínimo, máximo e a média de cada coluna.

Por fim, os três datasets foram concatenados e foi criada uma nova coluna contendo a informação se o cliente havia sido indicado por outro ou não.
