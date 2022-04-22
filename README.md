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

Perfil de geração

![image](https://user-images.githubusercontent.com/102811613/164726063-0fdbe902-20d2-46ca-abdd-c01742869832.png)
      
     
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

![image](https://user-images.githubusercontent.com/102811613/164726375-04965b02-22a8-4b9e-ad49-c40fdaf1981f.png)

2500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/164726406-fff9fea1-3587-43e0-b4e8-ea1540ef91d6.png)

5000 épocas - val loss (blue) and loss (orange)   

![image](https://user-images.githubusercontent.com/102811613/164726795-c7b93cb4-1306-4b2d-aa9a-41774aa61039.png)

5000 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/164726761-39ee88a9-62b8-4abe-9811-d090b85e6616.png)

7500 épocas - val loss (blue) and loss (orange)   

![image](https://user-images.githubusercontent.com/102811613/163681413-602067c8-9359-4ab7-ac0b-1c3bbe107631.png)

7500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/164727399-a9e6d8e4-f9d3-4991-8be5-2ed30847e96c.png)
 
•	Usina B:

Perfil de geração

![image](https://user-images.githubusercontent.com/102811613/164729906-65ac35ec-7faf-42bb-bae0-530062309359.png)

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
 
 ![image](https://user-images.githubusercontent.com/102811613/164733072-0388caae-b004-4aa1-9f8b-25252755c0c4.png)

 2500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/164733037-d811055d-4e21-4a9d-ad9e-fd344a247a0a.png)

 5000 épocas - val loss (blue) and loss (orange)   
 
![image](https://user-images.githubusercontent.com/102811613/164732489-7f9d3804-c1db-4ae0-bb52-c1e424ce4bc1.png)

 5000 épocas - previsão em verde
 
![image](https://user-images.githubusercontent.com/102811613/164732500-657b71fa-202a-43c9-886d-e75807fa3954.png)

7500 épocas - val loss (blue) and loss (orange)   

![image](https://user-images.githubusercontent.com/102811613/164731084-53022b65-ec6b-4a60-b1ed-55e1447ed125.png)

7500 épocas - previsão em verde

![image](https://user-images.githubusercontent.com/102811613/164731117-859551d0-9fa9-4c2f-974a-5fa240de23cf.png)

•	Usina C:

Perfil de geração

![image](https://user-images.githubusercontent.com/102811613/164733585-39cd057f-eb6b-4c3e-adee-27f8749a13dc.png)

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

![image](https://user-images.githubusercontent.com/102811613/164733843-2f87ac51-0641-46d3-b8f2-dc4bbe61f159.png)

2500 épocas - Realizado x Previsão 

![image](https://user-images.githubusercontent.com/102811613/164733864-47697955-4491-4c72-b3ad-92c198189db0.png)

5000 épocas - val loss (blue) and loss (orange)    

![image](https://user-images.githubusercontent.com/102811613/164735038-cd11252f-276c-4c37-aeda-0ff416b8f579.png)

5000 épocas - Realizado x Previsão

![image](https://user-images.githubusercontent.com/102811613/164735012-1daa4ca1-36bb-4acb-9c5f-2fa79bab31a3.png)

7500 épocas - val loss (blue) and loss (orange)    

![image](https://user-images.githubusercontent.com/102811613/164736318-bdb6c94a-d69a-418a-9b30-81412928205d.png)

7500 épocas - Realizado x Previsão 

![image](https://user-images.githubusercontent.com/102811613/164736345-abd5b364-c80a-45f8-9bc8-990c2827ef14.png)

•	Subsistema Nordeste:

Perfil de geração

![image](https://user-images.githubusercontent.com/102811613/164725258-7633574b-d528-43e7-92e9-3653d24d3e8d.png)
      
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

![image](https://user-images.githubusercontent.com/102811613/164721739-4664d2ad-ff0f-4a70-bd12-8453c68dcbcc.png)

2500 épocas - Realizado x Previsão 

![image](https://user-images.githubusercontent.com/102811613/164724865-c91878fa-a7f0-47d8-95fd-ac455c6cffb5.png)

5000 épocas - val loss (blue) and loss (orange)       

![image](https://user-images.githubusercontent.com/102811613/164722193-65d17962-549c-4310-9042-b2b92036974f.png)

5000 épocas - Realizado x Previsão 

![image](https://user-images.githubusercontent.com/102811613/164724339-7de844cc-8be8-4bdb-8caf-4347577fbf16.png)

7500 épocas      

![image](https://user-images.githubusercontent.com/102811613/164723415-bb981b0a-71fc-4be4-bc58-66a144ebf1de.png)

7500 épocas - Realizado x Previsão 

![image](https://user-images.githubusercontent.com/102811613/164723475-62828c6e-8511-4abe-b854-94cee877e39d.png)



### 4. Conclusões
Os melhores resultados obtidos indicaram que para as Usinas B e Co modelo consegue prever o perfil de geração até Y meses em relação ao realizado após janeiro de 2021. Expandindo a análise para diferente otimizadores de modelo, foi verificado que, em Z dos casos, o modelo consegue prever o perfil de geração com N% de “acerto” sobre a geração real das usinas e N2% para o Submercado.


---

Matrícula: 201.190.196

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
