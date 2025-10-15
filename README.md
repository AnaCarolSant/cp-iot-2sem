# CP-IOT - Repositório do Segundo Semestre

Este repositório contém dois projetos desenvolvidos no segundo semestre relacionados a inteligência artificial aplicada a IoT e visão computacional:

- redes neurais (notebook em `redes-neurais/redes_neurais_wine.ipynb`)
- visão computacional (notebook em `visao-computacional/visão_computacional_fruits.ipynb` e pasta `visao-computacional/imagem-reconhecer`)

## Integrantes

Lista de RMs dos integrantes:

- RM: [insira aqui o RM do integrante 1]
- RM: [insira aqui o RM do integrante 2]
- RM: [insira aqui o RM do integrante 3]

> Observação: substitua os itens acima pelos RMs reais dos integrantes do grupo.

## Projeto 1 — Redes Neurais

Resumo

O notebook `redes-neurais/redes_neurais_wine.ipynb` contém um experimento com redes neurais aplicado ao conjunto de dados Wine (ou outro dataset de classificação de vinhos). O objetivo é explorar pré-processamento, arquitetura de rede simples, treino e avaliação.

Conteúdo principal

- Carregamento e análise exploratória do dataset
- Pré-processamento (normalização/escala, divisão treino/validação/teste)
- Definição de uma rede neural (TensorFlow/Keras ou PyTorch conforme o notebook)
- Treinamento, salvamento de modelo e avaliação (matriz de confusão, métricas)

Como executar

1. Abra o notebook `redes-neurais/redes_neurais_wine.ipynb` no Google Colab ou localmente.
2. Instale dependências se necessário (por exemplo, `tensorflow`, `scikit-learn`, `pandas`, `matplotlib`).
3. Execute as células em sequência.

Notas

- Se executar localmente, uma GPU torna o treino mais rápido, mas para modelos pequenos do notebook a CPU também é aceitável.

## Projeto 2 — Visão Computacional

Resumo

O notebook `visao-computacional/visão_computacional_fruits.ipynb` e a pasta `visao-computacional/imagem-reconhecer` contêm o projeto de detecção/classificação de objetos com foco em frutas. O dataset usado para treinar o detector foi criado no Roboflow e exportado para o formato compatível com YOLOv8.

Dataset

- Origem: criado no Roboflow (anotações/labels geradas na interface do Roboflow).
- Formato: exportado para o formato YOLO (arquivos de imagem + arquivos .txt com bounding boxes e labels) — compatível com o Ultralytics YOLOv8.
- Observações: os arquivos de labels seguem o esquema de classes do Roboflow. Garanta que a estrutura de pastas esteja organizada como esperado pelo treinamento YOLO (por exemplo, `train/images`, `train/labels`, `valid/images`, `valid/labels`).

Treinamento (YOLOv8)

O modelo foi treinado com YOLOv8 por 10 épocas, que foi o ajuste usado para obter melhor desempenho no experimento deste projeto. Para reproduzir o treino, recomenda-se usar Google Colab com GPU.

Passos rápidos para treinar no Google Colab (recomendado com GPU)

1. Abra um novo notebook no Google Colab e ative a GPU: Menu `Runtime` → `Change runtime type` → `GPU`.
2. Instale o Ultralytics YOLOv8 e outras dependências:

```bash
pip install ultralytics roboflow
```

3. Faça upload do dataset exportado do Roboflow ou clone/baixe do repositório onde ele está salvo. A estrutura de pastas esperada é:

```
dataset/
	train/
		images/
		labels/
	valid/
		images/
		labels/
	data.yaml  # arquivo de configuração das classes e caminhos
```

4. Crie/edite o arquivo `data.yaml` com o caminho para os conjuntos e a lista de classes. Exemplo mínimo:

```yaml
train: /content/dataset/train/images
val: /content/dataset/valid/images
nc: 3
names: ['maçã','banana','laranja']
```

5. Execute o treinamento com YOLOv8 (usando a API Ultralytics):

```python
from ultralytics import YOLO

# carregar um modelo pré-treinado (por exemplo yolov8n)
model = YOLO('yolov8n.pt')

# treinar por 10 épocas
model.train(data='/content/dataset/data.yaml', epochs=10, imgsz=640, batch=16)
```

6. Após o término, os pesos estarão em `runs/detect/train/weights/` (ou caminho definido pela biblioteca). Baixe os arquivos de pesos e os resultados.

Dicas para melhor desempenho

- Use GPU (Colab/Local) para acelerar o treino.
- Ajuste `imgsz`, `batch`, `optimizer` e técnicas de augmentação conforme necessidade.
- Se o dataset for pequeno, considere aumentar epochs, usar transfer learning com modelos maiores (por exemplo `yolov8s.pt`) e aumentar a augmentação.

Reproduzindo o experimento localmente

1. Instale uma versão recente do Python (3.8+), crie um ambiente virtual e instale dependências:

```powershell
python -m venv .venv; .\.venv\Scripts\Activate.ps1; pip install -U pip
pip install ultralytics roboflow opencv-python-headless
```

2. Prepare o dataset com a mesma estrutura `data.yaml` e execute um script Python semelhante ao mostrado acima.

## Observações finais

- O dataset de visão computacional foi criado no Roboflow, anotado e exportado no formato YOLO. Os labels e as anotações são os que foram utilizados durante o treinamento com YOLOv8.
- O treinamento usado no experimento foi de 10 épocas, com o objetivo de obter melhor desempenho para o tamanho do dataset utilizado. Para geralizar melhor, recomenda-se testar mais épocas e validação cruzada quando possível.
- O ideal é rodar o treinamento em uma GPU — recomendamos Google Colab (GPU) para reprodutibilidade e rapidez.

## Arquivos importantes

- `redes-neurais/redes_neurais_wine.ipynb` — notebook do projeto de redes neurais
- `visao-computacional/visão_computacional_fruits.ipynb` — notebook do projeto de visão computacional
- `visao-computacional/imagem-reconhecer/` — scripts e recursos auxiliares para o projeto de visão

## Como contribuir

1. Atualize os notebooks com comentários claros.
2. Inclua os RMs reais na seção de Integrantes.
3. Se for adicionar o dataset ao repositório, coloque-o em `visao-computacional/dataset/` ou documente onde ele está hospedado (por exemplo, link do Roboflow ou Google Drive).

---

Se quiser, eu posso também preencher automaticamente a lista de RMs se você me fornecer os números, ou preparar um notebook Colab pronto para executar o treinamento com o dataset (basta me informar onde o dataset está hospedado - Google Drive, link do Roboflow export, ou arquivo ZIP).
