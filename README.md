# Projeto CIFAR-10

**Classificação de Imagens com Rede Neural Convolucional (CNN)**

#Grupo: 
| RA |GitHub | 
|-|-|
|2404245|[Carlos José Fernández Porto](https://github.com/Trasn0/Projeto-Cifar-10) |
|2400632|[Audrey Mayumi Narimatsu](https://github.com/AudreyNarimatsu/) |
|2404084|[Guilherme Martins Silva](https://github.com/GuilhermeMartinsSilva/) |
|2403783|[Mauricio Antonio dos Santos Souza](https://github.com/MAURICIOASSOUZA/Projeto-Cifar-10) |


## Descrição do Problema 
O objetivo deste projeto é construir e treinar uma rede neural convolucional (CNN) utilizando o conjunto de dados [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html). O CIFAR-10 é um dataset amplamente utilizado em aprendizado de máquina, que consiste em 60.000 imagens coloridas de 32x32 pixels, divididas em 10 classes diferentes. As classes incluem objetos como avião, carro, pássaro, gato, vaso, cachorro, sapo, cavalo, barco e caminhão. O desafio é criar um modelo capaz de classificar corretamente novas imagens com pelo menos **75% de acurácia no conjunto de teste**. 
[Veja o notebook completo no Google Colab](https://colab.research.google.com/drive/1PHYxb0Eeitfd-x2FncNRGizIIBzi4fVK ). 

## Passo a Passo da Implementação  
### 1. Carregamento e Pré-processamento dos Dados  
- **Carregamento dos Dados**: O dataset CIFAR-10 foi carregado usando a biblioteca keras.datasets.cifar10. O dataset é dividido automaticamente em conjuntos de treino (50.000 imagens) e teste (10.000 imagens).
- **Normalização**: As imagens foram normalizadas para valores entre 0 e 1, dividindo cada pixel pelo valor máximo (255), para facilitar o treinamento da rede neural.
- **One-Hot Encoding**: As etiquetas das classes foram convertidas em representação one-hot encoding, já que o problema é de classificação multiclasse.
     

### 2. Arquitetura da CNN
### Arquitetura da CNN
#### Estrutura geral:
| Camada                | Detalhes                                      |
|-----------------------|-----------------------------------------------|
| **Conv2D + BatchNorm** | 32 filtros, ReLU, padding "same"              |
| **MaxPooling + Dropout** | Pooling 2x2, Dropout 25%                    |
| **Conv2D + BatchNorm** | 64 filtros, ReLU, padding "same"              |
| **MaxPooling + Dropout** | Pooling 2x2, Dropout 25%                    |
| **Flatten + Dense**   | Dense(128) + Dropout 50%                     |
| **Saída**             | Dense(10) + Softmax                          |

#### Justificativa técnica:
- **Blocos Convolucionais**: 
  - Camadas `Conv2D` extraiem características locais da imagem, enquanto `BatchNormalization` estabiliza o treinamento ao normalizar as ativações.
  - O `Dropout` após o `MaxPooling` reduz overfitting, descartando aleatoriamente neurônios durante o treinamento.

- **Camadas Densas**:
  - A camada `Flatten` transforma as matrizes 2D em vetores 1D para compatibilidade com camadas densas.
  - O `Dropout` de 50% na camada densa é mais agressivo, pois redes densas são propensas a memorizar dados de treino.

- **Saída**: 
  - A ativação `Softmax` converte os valores de saída em probabilidades para as 10 classes do CIFAR-10.

### 3. Compilação e Treinamento  
- **Otimizador**: Usamos o **Adam** com taxa de aprendizado inicial de 0.001 por sua eficiência em problemas de classificação.
- **Função de Perda**: `Categorical Crossentropy`, adequada para problemas multiclasse.
- **Métrica**: A **acurácia** foi usada para monitorar o desempenho durante o treinamento.

### 4. Evitar Overfitting com Early Stopping  
- **Callback Early Stopping**: Implementou-se um callback para interromper o treinamento se a acurácia de validação não melhorar após 10 épocas consecutivas. Isso ajuda a evitar overfitting e garante que o modelo seja salvo no ponto em que apresenta o melhor desempenho. 

### 5. Treinamento do Modelo 
- **Parâmetros de Treinamento**:
    - Batch size: 64
    - Número de épocas: 10 (limitado pelo early stopping)
    - Dados de validação: Utilizados para monitorar o desempenho e decidir quando parar o treinamento.
         
- **Resultados do Treinamento**: O histórico de treinamento foi registrado para análise posterior.
     
### 6. Avaliação do Modelo 
Após o treinamento, o modelo foi avaliado no conjunto de teste para medir sua capacidade de generalização.
A acurácia final no conjunto de teste também é calculada e exibida.
     

### 7. Visualização dos Resultados 
**Gráfico de Desempenho**: um gráfico mostra a evolução da acurácia ao longo das épocas, tanto no conjunto de treino quanto no conjunto de teste. Isso permite analisar a convergência do modelo e verificar se há sinais de *overfitting* ou *underfitting*.
          

## Resultados 
   - **Acurácia no Teste**: 76.63% ✅ (superou o objetivo de 75%)
   - Gráfico de Desempenho:
![Acurácia de Treino vs. Teste](https://github.com/Trasn0/Projeto-Cifar-10/blob/main/grafico_acuracia.png)
    
## Conclusão 
O modelo de CNN desenvolvido demonstrou um bom desempenho na tarefa de classificação das imagens do dataset **CIFAR-10**. Com base nos resultados obtidos: 
   - A acurácia no conjunto de teste foi de 76.63% em 10 épocas, o que é considerado razoável para este tipo de problema.
   - O uso de técnicas como *dropout*, *batch normalization* e *early stopping* ajudou a evitar *overfitting* e melhorar a generalização do modelo.
   - O gráfico de desempenho mostra uma curva suave de aumento da acurácia no conjunto de treino, sem sinais claros de *overfitting*, indicando que o modelo está aprendendo de forma eficiente.
           
## Próximos passos: 
   - **Hiperparâmetros**: É possível explorar ajustes nos hiperparâmetros, como a taxa de aprendizado, número de filtros nas camadas convolucionais e configurações do dropout, para melhorar ainda mais o desempenho.
   - **Data Augmentation**: Aumentar artificialmente o tamanho do dataset através de técnicas de *data augmentation* pode ajudar a melhorar a robustez do modelo.
   - **Arquiteturas Mais Complexas**: Experimentar arquiteturas mais avançadas, como *ResNet* ou *VGG*, pode levar a resultados ainda melhores.
      

## Como Executar no Google Colab
1. Clique no botão [Open in Colab](https://colab.research.google.com/assets/colab-badge.svg ) acima.
2. No Colab, vá para `Runtime > Run All` para executar todas as células do notebook.
3. Para usar GPU (recomendado), ative em `Runtime > Change runtime type > Hardware accelerator: GPU`.

     
## Estrutura do Repositório 
```bash
├── Deep_Learnig_cifar10.ipynb  # Notebook principal
├── README.md                   # Este arquivo
└── grafico_acuracia.png        # Gráfico gerado
```


## Citação
Krizhevsky, A. (2009). Learning Multiple Layers of Features from Tiny Images. University of Toronto.
