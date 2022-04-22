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

Assim, após as rodadas geradas para cada item temos as seguintes resultados:

•	Usina A:
     
     Para 2500 épocas:
        Train > RMSE: 0.09 / MAPE: 1.31 
        Test  > RMSE: 0.09 / MAPE: 34.74 
      Para 5000 épocas:
        Train > RMSE: 0.09 / MAPE: 1.30  
        Test  > RMSE: 0.09 / MAPE: 34.52  
      Para 7500 épocas:
        Train > RMSE: 0.09 / MAPE: 1.31  
        Test  > RMSE: 0.09 / MAPE: 34.95   
        
2500 épocas - val loss (blue) and loss (orange)       

![image](https://user-images.githubusercontent.com/102811613/163443207-53068eab-15df-4dc7-8386-a13f5cad70d4.png)

2500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/163443192-7031712d-353d-4e96-8f47-8f9f1488ef99.png)

5000 épocas - val loss (blue) and loss (orange)       

![image](https://user-images.githubusercontent.com/102811613/163442752-41a1aaad-f4ef-4243-8ed5-cc8d869df243.png)

5000 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/163442777-b6bbc9c6-b4c4-44c6-b6a2-ea4b347d6844.png)

7500 épocas - val loss (blue) and loss (orange)       

![image](https://user-images.githubusercontent.com/102811613/163440815-7e6cd98a-6183-47b8-87be-74891745b52b.png)

7500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/163440839-b068e765-c7e9-4d3a-9900-917081f9647e.png)
        
•	Usina B:
     
     Para 2500 épocas:
        Train > RMSE: 0.13 / MAPE: 1.20 
        Test  > RMSE: 0.12 / MAPE: 1.30 
      Para 5000 épocas:
        Train > RMSE: 0.13   / MAPE: 1.11  
        Test  > RMSE: 0.13   / MAPE: 1.19   
      Para 7500 épocas:
        Train > RMSE: 0.13   / MAPE: 1.11  
        Test  > RMSE: 0.13   / MAPE: 1.19 
        
 2500 épocas - val loss (blue) and loss (orange)  
 
 ![image](https://user-images.githubusercontent.com/102811613/162583249-33b7e57a-2223-4ca8-98d3-ebd868765f74.png)
 
 2500 épocas - previsão em verde
 
![image](https://user-images.githubusercontent.com/102811613/162583269-4b5eaa9e-21b2-4159-b773-9f9ef40ef2a1.png)

 5000 épocas - val loss (blue) and loss (orange)   
 
![image](https://user-images.githubusercontent.com/102811613/163439738-05954d78-cc1a-451d-a1b7-6870c90c4daf.png)

 5000 épocas - previsão em verde
 
![image](https://user-images.githubusercontent.com/102811613/163439777-11dfa1fa-a0f3-4932-b356-1ddeb190fd27.png)

7500 épocas - val loss (blue) and loss (orange)   

![image](https://user-images.githubusercontent.com/102811613/163440368-4fa7c9ab-3fd0-44ac-ba7f-8be113417fb0.png)

7500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/163440407-9c9b95ea-2936-4168-bbf6-56990f7f7066.png)


•	Usina C:
      
      Para 2500 épocas:
        Train > RMSE: 0.16   / MAPE: 1.30 
        Test  > RMSE: 0.09   / MAPE: 1.32 
      Para 5000 épocas:
        Train > RMSE: 0.16   / MAPE: 1.44 
        Test  > RMSE: 0.09   / MAPE: 1.45 
      Para 7500 épocas:
        Train > RMSE: 0.16   / MAPE: 1.46
        Test  > RMSE: 0.09   / MAPE: 1.47  
2500 épocas - val loss (blue) and loss (orange)      

 ![image](https://user-images.githubusercontent.com/102811613/163681191-554b491e-17b6-4cfe-aa70-bd16fcfb27f8.png)

2500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/163681221-ab7cc3f4-82ca-4d0a-8351-7e7c6adb11e3.png)

5000 épocas - val loss (blue) and loss (orange)   

![image](https://user-images.githubusercontent.com/102811613/163681312-27e50ea6-df0e-44d9-a7f8-ca9da4d1afd1.png)

5000 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/163681308-a868cd07-ee5f-4fe0-b624-5fea8b77e37c.png)

7500 épocas - val loss (blue) and loss (orange)   

![image](https://user-images.githubusercontent.com/102811613/163681413-602067c8-9359-4ab7-ac0b-1c3bbe107631.png)

7500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/164711070-124735f1-9aab-4dd0-9f06-f2bc6e50cb48.png)

•	Subsistema Nordeste:


      
      Para 2500 épocas:
        Train > RMSE: 18.72  / MAPE: 1.42
        Test  > RMSE: 31.53 / MAPE: 1.68 
      Para 5000 épocas:
        Train > RMSE: 18.77  / MAPE: 1.42
        Test  > RMSE: 31.55  / MAPE: 1.69 
      Para 7500 épocas:
        Train > RMSE:  18.82  / MAPE: 1.69  
        Test  > RMSE:  31.57  / MAPE: 1.43      

2500 épocas - val loss (blue) and loss (orange)    

![image](https://user-images.githubusercontent.com/102811613/164709385-f7c3ab2d-0f51-4112-8ce4-5595f2bb976a.png)

2500 épocas - Realizado x Previsão 

![image](https://user-images.githubusercontent.com/102811613/164721035-725c8fb2-8e3e-41f7-b7a1-87d7b8cfd24c.png)

5000 épocas - val loss (blue) and loss (orange)       

![image](https://user-images.githubusercontent.com/102811613/164710460-0dfe2d46-c40f-40dc-9d4d-672c08d4af53.png)


![image](https://user-images.githubusercontent.com/102811613/164719987-8f963f77-17e4-41da-804c-ae1b46ec28c0.png)

7500 épocas      

![image](https://user-images.githubusercontent.com/102811613/164719443-a607ad00-484a-42ed-87d0-3691ff66dae6.png)


![image](https://user-images.githubusercontent.com/102811613/164719375-f2b74d72-d835-4b44-8c50-4cd75de9ec18.png)


Os melhores resultados obtidos indicaram que para as Usinas -  - o modelo consegue prever o perfil de geração até Y meses em relação ao realizado após janeiro de 2021. Expandindo a análise para diferente otimizadores de modelo, foi verificado que, em Z dos casos, o modelo consegue prever o perfil de geração com N% de “acerto” sobre a geração real das usinas e N2% para o Submercado.

Perfil de geração

![image](https://user-images.githubusercontent.com/102811613/164710665-d7959db5-5597-413f-870b-a2c49940faeb.png)

### 4. Conclusões


---

Matrícula: 201.190.196

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
