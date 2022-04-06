# PUC_Projeto
# Previsão de séries temporais sobre a Geração Eólica do Nordeste

#### Aluno: [Carlos Henrique Calvo Martinez(https://github.com/carlosMartinez93).
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Previsão de Séries Temporais de Geração Eólica](https://github.com/carlosMartinez93/PUC_Projeto/blob/main/Previsao_Geracao_Eolica.py).

---

### Resumo

No presente trabalho foi desenvolvido modelo preditivo visando identificar o perfil de geração de uma usina elétrica de fonte eólica.
O desenvolvimento deste modelo preditivo se deu através de uma rede neural sobre usinas eólicas e o conjunto inteiro do Submercado Nordeste.
Além disso, para treinamento, utilizou-se a geração sazonal no período de janeiro de 2016 até janeiro de 2021.

### Abstract

In the present work, a predictive model was developed to identify the generation profile of a wind power plant.
The development of this predictive model took place through a neural network over wind farms and the entire set of the Northeast Submarket.
In addition, for training, seasonal generation was used in the period from January 2016 to January 2021.

### 1. Introdução

Ao longo dos últimos anos, foi observado um comportamento específico das usinas eólicas que mostra uma variação destoante do seu perfil de geração diária e mensal. 
Com isso, os agentes do Setor Elétrico Brasileiro (SEB) iniciaram estudos com o intuito de prever geração destes tipos de usina de forma a otimizar o planejamento de rede e minimizar riscos associados ao atendimento da Carga.
A motivação é sem dúvidas uma estratégia essencial para os agentes aumentarem a confiança na fonte renovável, diminuírem os riscos financeiros e maximizarem a eficiência operacional das usina.
Sabe-se que a geração eólica possui grande relevância dado que a sua perspectiva para as importações é de crescimento, considerando que a energia eólica representa hoje 10,9% da matriz elétrica brasileira e a expectativa é que chegue a 13,6% ao fim de 2025.

Dado este cenário, o objetivo geral neste trabalho é auxiliar a previsão do perfil de geração das usinas eólicas para os agentes do SEB.
Mas, para ter uma resposta mais eficaz para esse objetivo geral, a sua aplicação do modelo de rede neural sobre três usinas eólicas do nordeste e sobre o perfil de geração do Nordeste entre três períodos diferentes.

### 2. Modelagem

O projeto, desenvolvido em Python, consistiu em criar um modelo de deep learning para a previsão da série temporal de geração das usinas eólicas.
Para o treinamento, utilizou-se um base de dados com 60 meses de geração fornecido pelo Histórico de Operação do Operador Nacional do Sistema (ONS).

De forma que a rede neural possa receber corretamente a base de dados, os seus valores foram transformados num vetor numpy.
Assim, a mesma base é separada em treino e teste, 70% e 30% respectivamente. Vale Ressaltar que a divisão não é arranjada de forma aleatória mas, sim, sequencial.
Em seguida, com o intuito de receber os valores preditivos, é criada um dataset com a base original deslocado em n meses.

A rede neural sequencial utilizou os otimizadores SGD, RMSPROP, Adam, Nadam e a função de ativação Relu.

Junto a isso, são criados 11 camadas na mesma arquitetura de rede neural que inclui:
5 LSTM (Long Short Time Memory): Com 128, 64, 32, 16 e 8 neurônios, respectivamente. A primeira - de 128 neurônios - recebe também o vetor de look back. Camada responsável por "aprender" a dependência temporal de longa duração na série;
5 Dropout: Camada para ajudar na capacidade de generalização da rede, prevenindo o overffiting do modelo. Esta camada de dropout possui 20% de chance de ativação, isto é, durante a realziação do treinamento, o output de um neorônio terá 20% de chance do seu valor ser substituido por "0". Desta maneira, um neurônio não vai ficar "especializado" durante o treinaemnto ajudando assim a combater o overfitting do modelo;
1 Dense: A camada dense é responsável por resolver o problema de forma não linear. Essa camada é responsável por passar o resultado produzido por um neurônio em uma função não linear, possibilitando assim a resolução de problemas complexos e não lineares. Essa camada foi configurada com 100 neurônios e possui a função de ativação "relu";

E foram alternadas três quantidades de épocas de 2500, 5000 e 7500.

Por fim, foram utilizados as métricas de erro RMSE e MAPE visto a frequência utilização nos modelos de previsão de séries temporais de usinas eólicas.

### 3. Resultados

Os melhores resultados obtidos indicaram que, em X% dos casos, o modelo consegue prever o perfil de geração até Y meses em relação ao realizado após janeiro de 2021. Expandindo a análise para diferente otimizadores de modelo, foi verificado que, em Z dos casos, o modelo consegue prever o perfil de geração com N% de “acerto” sobre a geração real das usinas e N2% para o Submercado.

### 4. Conclusões


---

Matrícula: 201.190.196

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
