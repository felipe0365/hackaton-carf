# 🚗 Projeto de Previsão de Horas de Execução de Processos (HET)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://python.org)
[![Machine Learning](https://img.shields.io/badge/ML-Scikit--learn-orange.svg)](https://scikit-learn.org)

## 📋 Visão Geral

Este projeto implementa um sistema de **Machine Learning** para previsão de **Horas de Execução de Processos (HET)** baseado em características binárias de processos industriais. O objetivo é desenvolver modelos preditivos capazes de estimar o tempo necessário para execução de processos com base em suas características específicas.

## 🎯 Objetivo

Prever as horas de execução de processos industriais utilizando características binárias (presença/ausência de determinadas propriedades), permitindo melhor planejamento e otimização de recursos operacionais.

## 📊 Dataset

-   **Arquivo principal**: `Horas_parametros.xlsx`
-   **Amostras de treinamento**: 9.999 processos com valores HET conhecidos
-   **Amostras para previsão**: 10.743 processos sem valores HET
-   **Características**: 295 variáveis binárias (0/1) representando diferentes propriedades dos processos
-   **Variável alvo**: HET (Horas de Execução de Processos)

## 🔧 Tecnologias Utilizadas

-   **Python 3.x**
-   **Pandas** - Manipulação de dados
-   **NumPy** - Computação numérica
-   **Scikit-learn** - Machine Learning
-   **XGBoost** - Gradient Boosting
-   **SHAP** - Interpretabilidade de modelos
-   **Matplotlib/Seaborn** - Visualização
-   **Joblib** - Serialização de modelos

## 🚀 Metodologia

### 1. **Análise Exploratória de Dados (EDA)**

-   Análise de correlação ponto-bisserial entre características binárias e HET
-   Identificação das 20 características mais correlacionadas
-   Tratamento de valores ausentes

### 2. **Preparação dos Dados**

-   Separação entre conjunto de treinamento (com HET) e previsão (sem HET)
-   Divisão train/test (80/20) para validação
-   Preenchimento de valores ausentes com 0

### 3. **Modelagem Comparativa**

Foram testados **5 algoritmos diferentes** com otimização de hiperparâmetros:

#### 🥇 **Huber Regressor** (Vencedor)

-   **R²**: 0.7518
-   **MAE**: 5.1788 horas
-   **RMSE**: 7.8024 horas
-   **Vantagem**: Robusto a outliers, melhor performance geral

#### 🥈 **Lasso Regression**

-   **R²**: 0.7420
-   **MAE**: 5.3086 horas
-   **RMSE**: 7.9548 horas
-   **Vantagem**: Seleção automática de características (108 de 295)

#### 🥉 **Rede Neural (MLP)**

-   **R²**: 0.7417
-   **MAE**: 5.2303 horas
-   **RMSE**: 7.9583 horas
-   **Vantagem**: Captura relações não-lineares

#### **XGBoost**

-   **R²**: 0.7361
-   **MAE**: 5.3517 horas
-   **RMSE**: 8.0442 horas

#### **Random Forest**

-   **R²**: 0.7257
-   **MAE**: 5.4350 horas
-   **RMSE**: 8.2022 horas

### 4. **Otimização de Hiperparâmetros**

-   **Validação cruzada**: 5-fold
-   **Métrica de avaliação**: RMSE negativo
-   **Grid Search** para cada algoritmo

### 5. **Interpretabilidade**

-   **SHAP Values** para análise de importância das características
-   **Análise de coeficientes** (modelos lineares)
-   **Visualizações** de distribuição de erros

## 📈 Principais Descobertas

### Características Mais Importantes

1. **01.02** - Maior correlação positiva (0.6626)
2. **03.01** - Maior correlação negativa (-0.5460)
3. **01.07.01** - Correlação negativa significativa (-0.4828)

### Insights do Modelo

-   **Relação predominantemente linear** entre características e HET
-   **Huber Regressor** se destacou pela robustez a outliers
-   **Modelos lineares** superaram algoritmos baseados em árvores
-   **108 características** selecionadas pelo Lasso como mais relevantes

## 🛠️ Como Executar

### Pré-requisitos

```bash
# Instalar dependências principais
pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn joblib openpyxl

# Ou usar o arquivo requirements.txt (se disponível)
pip install -r requirements.txt
```

### Dependências Principais

-   `pandas>=1.3.0` - Manipulação de dados
-   `numpy>=1.21.0` - Computação numérica
-   `scikit-learn>=1.0.0` - Machine Learning
-   `xgboost>=1.5.0` - Gradient Boosting
-   `shap>=0.40.0` - Interpretabilidade
-   `matplotlib>=3.5.0` - Visualização
-   `seaborn>=0.11.0` - Visualização estatística
-   `joblib>=1.1.0` - Serialização
-   `openpyxl>=3.0.0` - Leitura de Excel

### Execução do Script Principal

```bash
python script_final.py
```

### Execução do Notebook

```bash
jupyter notebook notebook_v2.ipynb
```

## 📊 Resultados

### Performance Final

O **Huber Regressor** foi escolhido como modelo final por apresentar:

-   ✅ Maior R² (0.7518)
-   ✅ Menor MAE (5.18 horas)
-   ✅ Menor RMSE (7.80 horas)
-   ✅ Maior robustez a outliers

### Previsões Geradas

-   **10.743 previsões** de HET para processos sem valores conhecidos
-   **Arquivo de saída**: `Horas_parametros_predicted.xlsx`
-   **Modelo salvo**: `modelo_huber_final.joblib`

## 🔍 Interpretabilidade

### SHAP Analysis

-   **Característica 01.02**: Aumenta significativamente o tempo (+20 horas)
-   **Característica 03.01**: Diminui o tempo (-5 horas)
-   **Padrões lineares**: Relações claras entre características e HET

### Distribuição de Erros

-   **Concentração em torno de zero**: Modelos sem viés significativo
-   **Huber**: Menor dispersão de erros
-   **Robustez**: Melhor performance em casos extremos

## 📝 Conclusões

1. **Modelo Linear Robusto**: Huber Regressor é ideal para este problema
2. **Características Relevantes**: 108 de 295 características são significativas
3. **Performance Sólida**: R² de 0.75 indica boa capacidade preditiva
4. **Aplicabilidade**: Modelo pode ser usado para planejamento operacional

## 👥 Contribuição

Este projeto foi desenvolvido como parte de um hackathon, focando em:

-   Análise exploratória robusta
-   Comparação sistemática de algoritmos
-   Interpretabilidade dos resultados
-   Documentação completa

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

---

<div align="center">

[![Made with Python](https://img.shields.io/badge/Made%20with-Python-blue.svg)](https://python.org)
[![Powered by Scikit-learn](https://img.shields.io/badge/Powered%20by-Scikit--learn-orange.svg)](https://scikit-learn.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

</div>
