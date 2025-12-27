Visão geral
Este projeto compara diferentes modelos de aprendizado de máquina para classificar o tipo de pavimento (por exemplo, asfalto, paralelepípedo, terra) e a qualidade da via (boa, regular, ruim) usando dados de sensores instalados em veículos a partir do dataset Passive Vehicular Sensors (PVS).
​
O trabalho foi desenvolvido como projeto da disciplina de Redes Neurais, explorando modelos clássicos (Random Forest, MLP, SVM) e redes LSTM em uma arquitetura em dois estágios, onde a predição do tipo de pavimento é utilizada como entrada adicional para a classificação de qualidade.
​

Objetivos do projeto
Classificar o tipo de pavimento a partir de leituras de sensores veiculares (acelerômetros, entre outros) do conjunto de dados PVS.
​

Classificar a qualidade da via em três níveis (boa, regular, ruim), considerando o desbalanceamento das classes e a importância da identificação correta de segmentos em condição ruim.
​

Comparar o desempenho de Random Forest, Multi-Layer Perceptron, Support Vector Machine e Long Short-Term Memory em ambas as tarefas.
​

Avaliar uma arquitetura em cascata na qual a saída prevista do tipo de pavimento é usada como feature adicional para o modelo de qualidade.
​

Conjunto de dados
Fonte: Passive Vehicular Sensors (PVS), disponibilizado publicamente (Kaggle), contendo leituras de sensores de três veículos, três motoristas e nove cenários de condução.
​

Variáveis: sinais de aceleração em diferentes eixos/posições no veículo, timestamp e rótulos de tipo de pavimento e indicadores de qualidade de via.
​

Pré-processamento:

Criação de target_pavimento (3 classes) e target_qualidade (boa, regular, ruim) a partir de colunas binárias de qualidade.
​

Normalização/escala dos atributos e divisão em conjuntos de treino, validação e teste.
​

Preparação de janelas temporais de 20 passos para os modelos LSTM.
​

Modelos implementados
Random Forest (RF): utilizado tanto para tipo de pavimento quanto para qualidade, explorando número de árvores e profundidade para obter alta acurácia com baixo custo computacional.
​

Multi-Layer Perceptron (MLP): rede neural feedforward com duas camadas ocultas, ajustada para capturar relações não lineares entre as features de sensores e os rótulos de pavimento/qualidade.
​

Support Vector Machine (SVM): usado com kernel radial (RBF) para separar as três classes em espaços não lineares, alcançando bom desempenho especialmente na tarefa de pavimento.
​

Long Short-Term Memory (LSTM): rede recorrente aplicada às sequências temporais de sensores, explorando dependências temporais para melhorar a classificação, principalmente em qualidade da via.
​

Arquitetura em dois estágios (cascata)
Estágio 1 – Tipo de pavimento:

Entrada: features de sensores processadas.

Saída: rótulos previstos de tipo de pavimento para cada amostra (por modelo: RF, MLP, SVM, LSTM).
​

Estágio 2 – Qualidade da via:

Entrada: mesmas features de sensores + colunas adicionais com o tipo de pavimento previsto.

Saída: qualidade da via (boa, regular, ruim).
​

Justificativa: a qualidade percebida do pavimento depende do tipo de superfície, e utilizar a predição de pavimento como entrada ajuda o modelo de qualidade a capturar essa dependência conceitual.
​

Estrutura do repositório
Sugestão alinhada com a organização já utilizada:
​

Pavimento/

Scripts de EDA, pré-processamento, divisão de dados e treinamento dos modelos RF, MLP, SVM, LSTM para tipo de pavimento.
​

Qualidade/

Scripts de criação de target_qualidade, pré-processamento, montagem de datasets com pavimento previsto e treinamento dos modelos para qualidade da via.
​

data/ ou archive/PVS 9/

Dados brutos do PVS e versões intermediárias/finais (*_pronto.csv, X_train*.csv, X_test*.csv).
​

results/

Matrizes de confusão, métricas (acurácia, precisão, recall, F1) e tabelas consolidadas usadas no artigo e na apresentação.
​

article/

Arquivo LaTeX baseado no template SBC com o artigo completo do projeto.
​

presentation/

Slides da apresentação de 10 minutos com roteiro sobre problema, metodologia, resultados e aplicações.
​

Como executar
Configurar o ambiente Python (versão 3.10) com as dependências de ciência de dados e deep learning (por exemplo, NumPy, pandas, scikit-learn, TensorFlow/Keras).

Definir o caminho para o dataset PVS nas variáveis de configuração (DATAPATH, PROJECT_ROOT) no arquivo de configuração do projeto.
​

Executar os scripts da pasta Pavimento/ para gerar modelos treinados e predições de tipo de pavimento.
​

Executar os scripts da pasta Qualidade/ para montar os datasets com pavimento previsto e treinar os modelos de qualidade.
​

Consultar os arquivos em results/ para analisar as métricas comparativas entre os modelos em cada tarefa.
​

Se quiser, na próxima mensagem dá para adaptar esse README para o formato exato do seu GitHub (por exemplo, acrescentando comandos python arquivo.py específicos de cada script).
