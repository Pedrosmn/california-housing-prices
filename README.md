# California Housing Prices Prediction 🏡📊

Este projeto realiza a análise exploratória e a modelagem preditiva dos valores médios de imóveis na Califórnia, com base nos dados de censo. O objetivo principal é construir modelos de regressão para estimar o `median_house_value`.

## 🗂️ Sobre os Dados
Os dados foram obtidos através do Kaggle (`camnugent/california-housing-prices`). O dataset original possui 20.640 instâncias e 10 atributos:
- **Variáveis de localização**: `longitude`, `latitude`, `ocean_proximity`
- **Características do bloco/imóvel**: `housing_median_age`, `total_rooms`, `total_bedrooms`
- **Informações demográficas e econômicas**: `population`, `households`, `median_income`
- **Variável Alvo (Target)**: `median_house_value`

## 🛠️ Etapas de Processamento (Pipeline)
1. **Análise Exploratória de Dados (EDA)**: Identificação de dados faltantes e visualização das distribuições (com auxílio de boxplots e histogramas).
2. **Engenharia de Variáveis**: Aplicação de *One-Hot Encoding* na variável categórica `ocean_proximity`.
3. **Tratamento de Anomalias**: O gráfico de distribuição evidenciou dados censurados (limite em \$ 500.001,00). As instâncias com esse teto foram excluídas da amostra de treino e de teste para não enviesar o aprendizado do modelo.
4. **Imputação de Ausentes**: Preenchimento de 207 valores nulos (NaN) na coluna `total_bedrooms` pela média da base de treino (`SimpleImputer`).
5. **Normalização**: Padronização dos dados numéricos para a mesma escala utilizando o `StandardScaler`.

## 🤖 Modelos Avaliados
Para estabelecer um termo de comparação, a amostra de treino (70%) e teste (30%) foi aplicada a quatro aproximações diferentes:
1. **Dummy Regressor** (Modelo Base/Baseline usando a estratégia da média)
2. **Regressão Linear Múltipla**
3. **Árvore de Decisão** (Decision Tree Regressor)
4. **Random Forest Regressor**

## 📈 Resultados
Abaixo está o desempenho comparativo dos modelos no conjunto de teste. O conjunto **Random Forest** obteve a melhor generalização e os menores erros de previsão:

| Modelo | MAE | RMSE | R² |
| :--- | :--- | :--- | :--- |
| Dummy Model | 78.275,75 | 97.734,71 | 0,00 |
| Regressão Linear | 44.943,43 | 60.772,94 | 0,61 |
| Árvore de Decisão | 41.568,28 | 62.741,99 | 0,59 |
| **Random Forest** | **30.061,25** | **44.621,21** | **0,79** |

## 🔑 Importância das Features
Avaliando a importância de atributos (*Feature Importances*) extraída do Random Forest, os 5 fatores que mais pesaram no valor das casas foram:
1. `median_income` (43,1%)
2. `ocean_proximity_INLAND` (16,1%)
3. `longitude` (12,0%)
4. `latitude` (11,1%)
5. `housing_median_age` (4,8%)

## 💻 Tecnologias e Bibliotecas Utilizadas
* `Python` (Jupyter Notebook)
* `Pandas` e `NumPy` para manipulação de dados
* `Scikit-Learn` para pipeline de machine learning e métricas
* `Matplotlib`, `Seaborn` e `Missingno` para análise e visualização gráfica
* `Kagglehub` para download integrado do dataset
