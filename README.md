# MVP-2--Seguranca-Cibernetica
Deteccao de trafego malicioso em dispositivos IoT

# RT-IoT2022 - Projeto de Machine Learning

## 1. Definição do Problema

**Objetivo:** Entender e descrever claramente o problema de detecção de tráfego malicioso em dispositivos IoT.

* **Descrição do problema:** O objetivo principal é classificar o tráfego de rede de dispositivos IoT em benigno ou malicioso, permitindo a detecção precoce de ataques cibernéticos, como negação de serviço, exploração de vulnerabilidades e acesso não autorizado. Este problema é crítico para a segurança de dispositivos conectados, especialmente em ambientes industriais e residenciais inteligentes, onde falhas podem ter impacto financeiro e operacional significativo.
* **Premissas/Hipóteses:** Supõe-se que padrões de tráfego malicioso possuem características distintas do tráfego benigno, e que essas diferenças podem ser capturadas por atributos de rede como número de pacotes, tamanhos de payload, protocolos e comportamentos temporais. Também assume-se que os ataques presentes no dataset representam os principais tipos de intrusão em IoT.
* **Restrições/Condições:** A seleção de dados considerou apenas atributos relevantes à análise de tráfego, excluindo identificadores irrelevantes como endereços IP de origem ou destino, que poderiam introduzir viés. Foram mantidas apenas instâncias com rótulos claramente definidos, garantindo consistência para treinamento e avaliação.
* **Descrição do Dataset:** O RT-IoT2022 contém aproximadamente 123.000 instâncias e 83 atributos de rede, incluindo contagens de pacotes, portas, protocolos, flags de TCP, métricas temporais, entre outros. Cada instância possui um rótulo indicando se o tráfego é benigno ou se representa um tipo específico de ataque. O dataset é tabular, adequado para aplicação de modelos clássicos de Machine Learning.

## 2. Preparação de Dados

**Objetivo:** Realizar operações de preparação dos dados para modelagem, garantindo qualidade e consistência.

* **Separação treino/teste:** O dataset foi dividido em 80% para treino e 20% para teste, mantendo a proporção original das classes (estratificação). Esta abordagem assegura que o modelo tenha exemplos suficientes de todas as classes e que a avaliação seja representativa.
* **Validação cruzada:** Foi utilizada validação cruzada estratificada (5 folds) para avaliar a performance dos modelos de forma robusta, mitigando variância causada por amostras específicas e garantindo generalização.
* **Transformações de dados:** Todos os atributos numéricos foram padronizados para média zero e desvio padrão um, evitando que escalas diferentes impactem a performance dos modelos. Variáveis categóricas foram codificadas usando LabelEncoder. Visualizações, como histogramas, boxplots e heatmaps de correlação, foram geradas para análise exploratória.
* **Feature selection:** Foram descartadas colunas irrelevantes ou altamente correlacionadas, mantendo atributos que contribuem significativamente para a classificação. Essa seleção reduz a dimensionalidade, melhora a interpretabilidade e aumenta a performance dos modelos.

## 3. Modelagem e Treinamento

**Objetivo:** Construir modelos de Machine Learning para classificação do tráfego.

* **Algoritmos selecionados:** Random Forest, Gradient Boosting, Logistic Regression, SVM e KNN. Justificativa: estes algoritmos são adequados para dados tabulares, oferecem robustez contra overfitting, interpretabilidade parcial (como em Random Forest) e comprovada eficácia em problemas de classificação com múltiplos atributos.
* **Ajuste inicial de hiperparâmetros:** Inicialmente foram utilizados parâmetros padrão para todos os modelos. Posteriormente, hiperparâmetros críticos (como número de estimadores e profundidade máxima em Random Forest, taxa de aprendizado em Gradient Boosting, C e kernel em SVM) foram otimizados via GridSearchCV.
* **Treinamento:** Modelos foram treinados utilizando pipelines, que incluem padronização dos dados e otimização de hiperparâmetros. A validação cruzada estratificada garante que o modelo aprenda padrões robustos sem sobreajustar dados específicos.
* **Otimização de hiperparâmetros:** Realizada usando GridSearchCV com validação cruzada. Cada parâmetro foi justificado por relevância na performance do modelo, garantindo que a otimização seja eficiente e consistente.
* **Métodos avançados:** Além dos modelos individuais, ensembles (Random Forest e Gradient Boosting) foram avaliados por sua capacidade de combinar múltiplos aprendizados e reduzir variância.
* **Comitê de modelos:** É possível implementar ensemble de diferentes algoritmos (voting ou stacking) para explorar complementaridades e aumentar a robustez do sistema de detecção.

## 4. Avaliação de Resultados

**Objetivo:** Analisar o desempenho dos modelos em dados não vistos, garantindo confiabilidade e generalização.

* **Métricas de avaliação:** Acurácia, precision, recall, F1-score e matriz de confusão foram escolhidas por sua relevância em classificação binária e pelo possível desbalanceamento das classes. Estas métricas permitem avaliar tanto a capacidade de detectar ataques quanto de evitar falsos positivos.
* **Treinamento e teste:** Cada modelo foi treinado com toda a base de treino e avaliado no conjunto de teste, garantindo que a avaliação represente dados não vistos.
* **Resultados:** Modelos ensemble (Random Forest e Gradient Boosting) apresentaram melhor acurácia, menor variância e maior equilíbrio entre precisão e recall, confirmando as hipóteses iniciais.
* **Overfitting:** Alguns modelos simples, como SVM e KNN, mostraram tendência a overfitting com parâmetros padrão, mitigada pelo ajuste e padronização.
* **Comparação entre modelos:** Ensembles performaram melhor, seguidos por Logistic Regression, com KNN e SVM apresentando menor desempenho em métricas agregadas.
* **Melhor solução:** Random Forest otimizado via GridSearchCV, com validação cruzada e padronização, foi identificado como o modelo final mais robusto, confiável e interpretável para detecção de tráfego malicioso em IoT.
