# Atividade — Treinamento de Redes Neurais com Keras (Dados Tabulares)

Este repositório contém os exercícios solicitados para o checkpoint.

Estrutura:

- `Exercise1_classification.py` — Classificação multiclasses no Wine dataset (UCI). Treina um modelo em Keras
  (2 camadas ocultas com 32 neurônios) e compara com um RandomForestClassifier do scikit-learn. Imprime
  métricas de acurácia e relatórios de classificação.
- `Exercise2_regression.py` — Regressão no California Housing dataset. Treina um modelo em Keras
  (3 camadas ocultas: 64, 32, 16) e compara com LinearRegression e RandomForestRegressor. Imprime RMSE/MAE.
- `requirements.txt` — dependências sugeridas para reproduzir os experimentos.

Como rodar

1. Crie um ambiente virtual (recomendado) e instale dependências:

   python -m venv .venv; .\.venv\Scripts\Activate.ps1; pip install -r atividade\requirements.txt

2. Execute os scripts:

   python atividade\Exercise1_classification.py
   python atividade\Exercise2_regression.py

Notas e Discussão

- Ambos os scripts usam divisão treino/teste com random_state fixo para reprodutibilidade.
- Para classificação, convertemos as labels para one-hot ao treinar com Keras e usamos
  categorical_crossentropy como perda, conforme solicitado.
- Para regressão, reportamos RMSE e MAE; o modelo com menor RMSE é considerado melhor.

Resultados

- Os resultados podem variar levemente entre execuções devido a inicialização aleatória e amostragem.
- Recomenda-se executar várias sementes e/ou usar cross-validation para uma comparação mais robusta.

Licença: MIT
