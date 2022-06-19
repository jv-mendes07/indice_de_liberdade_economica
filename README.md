# Índice de Liberdade Econômica (EDA)

Neste projeto, apresento em detalhes uma análise exploratória atinente ao conjunto de dados do Índice de Liberdade Econômica (Index of Economic Freedom), que é uma pesquisa de ranqueamento que visa saber quais são os países mais livres no âmbito econômico e quais não são, além de que tal pesquisa estatística expõe como a liberdade econômica impacta notavelmente na riqueza de uma população.

As ferramentas utilizadas nesta análise exploratória foram Python como linguagem programática, Pandas como biblioteca para manipulação de dados, e por fim às bibliotecas Matplotlib e Seaborn foram utilizáveis conjuntamente para realizar plotagens de gráficos que expusessem com mais facilidade às informações que foram extraídas do conjunto de dados.

## Importação de Bibliotecas

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

```

## Fonte de dados

O dataset [2022 Index Of Economic Freedom](https://www.heritage.org/index/explore) utilizado em tal análise exploratória está hospedado disponivelmente no site da Index Heritage Foundation para uso gratuito.

## Importação do Dataset 

Antes de podermos exportar o conjunto de dados, tivemos que instalar o pacote xlrd para exportarmos o dataset que estava configurado no formato .xlsx.

```
df = pd.read_excel('/content/drive/MyDrive/index2022_data.xls')
```
## Colunas do dataset

As colunas que estão contidas no conjunto de dados do índice de liberdade econômica são:

```
['pais_id', 'pais', 'webname', 'regiao', 'ranking_mundial',
       'ranking_regional', 'pontuacao_2022', 'direitos_de_propriedade',
       'eficiencia_juridica', 'integridade_governamental', 'carga_tributaria',
       'gastos_do_governo', 'saude_fiscal', 'liberdade_de_negocios',
       'liberdade_de_trabalho', 'liberdade_monetaria', 'liberdade_comercial',
       'liberdade_de_investimento', 'liberdade_financeira', 'taxa_tarifaria',
       'sem_nome', 'taxa_imposto_de_renda', 'taxa_de_imposto_corporativo',
       '%_carga_tributacao_pib', 'sem_nome_2', '%_despesas_gov_do_pib',
       'pais_2', 'sem_nome_3', 'populacao_milhoes', 'pib_bilhoes_per_capita',
       '%_crescimento_pib', '%_crescimento_pib_em_cinco_anos',
       'pib_per_capita', '%_de_desemprego', '%_de_inflacao',
       'entrade_de_ide_milhoes', '%_divida_publica_pib']
```       

## Processo de exploração dos dados

### **(1)** Tratamento dos dados

* Exclusão de colunas:

     **(1)** Antes de começarmos a exploração nos dados, tivemos que selecionar às colunas que seriam ou poderiam ser exploradas durante esse processo de análise, de antemão foi perceptível que há colunas que não serão exploráveis, e que à melhor opção seria com que tais colunas fossem excluídas, para que no processo analítico tivéssemos somente às colunas que poderiam ser do nosso interesse informacional.
 
   Tais colunas que foram excluídas, foram: 
   
   ```
   'webname', 'sem_nome_2', 
                   'pais_2', 'sem_nome_3', 'sem_nome'
   ```
* Seleção de índice:

    **(1)** Como temos uma coluna 'pais_id' que serve como identificador de cada país que foi analisado em tal pesquisa, então substituímos o índice automático criado pelo Pandas, para indexarmos a coluna 'pais_id' em seu lugar, justamente para não termos duas colunas de índices no dataset.
 
 
   ```
   df.set_index('pais_id', inplace = True)
   ```
 
 * Renomeação de coluna:

    **(1)** As colunas originalmente estavam escritas em inglês, porém traduzimos o nome das colunas para termos um entendimento mais claro e intuitivo do que cada coluna trata.
 
 * Criação de coluna:

    **(1)** Criamos a coluna 'avaliacao_final' para classificarmos quais são os países majoritariamente livres ou não-livres, moderadamente livres ou reprimidos, tal classificação foi feita com base nos critérios avaliativos da Index Heritage Foundation:
  
     **(a)** Países com uma pontuação de liberdade econômica entre 0 e 49.9 são classificados como países reprimidos, isto é, são países com baixa liberdade econômica.
  
     **(b)** Países com uma pontuação de liberdade econômica entre 50 e 59.9 são classificadamente países não-livres economicamente.
  
     **(c)** Países com uma pontuação de liberdade econômica entre 60 e 69.9 são classificadamente países moderadamente livres.
  
     **(d)** Países com uma pontuação de liberdade econômica acima de 70 são classificados como países majoritariamente livres, isto é, são países com alta liberdade econômica.
  
### **(2)** Conhecimento exploratório dos dados

Antes de começarmos à extrair em detalhes ás informações de tal conjunto de dados, precisamos esclarecer o conceito de liberdade econômica.

Basicamente, um país é considerado livre economicamente se e somente se tal país não tiver ou tiver pouquíssimas regulamentações burocráticas que impeçam a iniciativa privada de funcionar.

Em suma um país é livre economicamente se o estado não intervir exageradamente na economia, por exemplo:

   **(a)** Se tal país não tiver regulamentações empresariais e trabalhistas que impeçam um empreendedor de abrir um negócio ou que impeçam um trabalhador de ser contratado. 
  
   **(b)** Se tal país não tiver um estado 'inchado' que atue em vários setores econômicos, e que impeça a iniciativa privada de atuar em tais setores.
  
   **(c)** Se tal país tiver baixas cargas tributárias ao ponto de aumentar o custo de produção dos empreendedores e impedi-los de investir.
  
Tais critérios citáveis acima, são um dos critérios que poderão influenciar para que um país seja considerado livre economicamente, um país majoritariamente livre, por exemplo, não precisa preencher todos os critérios acima, mas terá que preencher um ou dois de tais critérios citados.

À partir de tal explicação prévia do que é liberdade econômica, podemos começar tal análise exploratória, primariamente iremos responder uma questão simples de quais países e regiões mundiais que foram inclusos em tal pesquisa, e em qual proporção:

#### **(1)** Quantos países foram inclusos em tal pesquisa do índice de liberdade econômica?


