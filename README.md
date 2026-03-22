# Tech Challenge Fase 3 — Previsão de Atrasos de Voos nos EUA
**Machine Learning Engineering — Pós Tech FIAP**

---

## Objetivo

Aplicar técnicas de Machine Learning supervisionado e não supervisionado para analisar e prever atrasos de voos nos Estados Unidos, utilizando um dataset com aproximadamente 5,8 milhões de registros de 2015.

---

## Estrutura do Projeto

```
tech-challenge-fase3/
│
├── tech_challenge_fase3.ipynb   # Notebook principal com todo o código
└── README.md                    # Este arquivo
```

---

## Dataset

O dataset não está incluído neste repositório por restrição de tamanho do GitHub (565 MB). Para reproduzir o projeto:

1. Acesse [Flight Delays — Kaggle](https://www.kaggle.com/datasets/usdot/flight-delays)
2. Faça download dos três arquivos: `flights.csv`, `airports.csv` e `airlines.csv`
3. Coloque os três arquivos na mesma pasta do notebook
4. Ajuste a variável `PASTA` na célula de carregamento para o caminho correto

---

## Como Executar

### Localmente (Jupyter Notebook)

```bash
# Instalar dependências
pip install pandas numpy matplotlib seaborn scikit-learn

# Abrir o notebook
jupyter notebook tech_challenge_fase3.ipynb
```

### Google Colab

1. Faça upload do notebook no [Google Colab](https://colab.research.google.com)
2. Coloque os três CSVs numa pasta do Google Drive
3. Atualize a variável `PASTA` na célula de carregamento com o caminho da sua pasta
4. Execute todas as células em ordem

---

## Abordagem

### 1. Exploração dos Dados (EDA)
- Análise de valores ausentes e estratégia de limpeza
- Identificação e remoção de aeroportos com código numérico inválido
- 5 visualizações para responder perguntas específicas sobre o problema
- Matriz de correlação para identificar variáveis redundantes e data leakage

### 2. Modelagem Supervisionada — Classificação
- **Objetivo:** prever se um voo vai atrasar mais de 15 minutos (padrão DOT/EUA)
- **Algoritmos comparados:** Regressão Logística vs Random Forest
- **Problema identificado e corrigido:** desbalanceamento de classes (82% vs 18%) resolvido com `class_weight='balanced'`
- **Métrica prioritária:** Recall — preferível alertar um atraso que não ocorra a deixar de alertar um atraso real
- **Resultado:** Random Forest com Recall de 0.70 e F1-Score de 0.38

### 3. Modelagem Não Supervisionada — K-Means
- **Objetivo:** agrupar aeroportos por perfil operacional de atraso
- **Número de clusters:** k=3, definido pelo Método do Cotovelo
- **Visualização:** PCA para redução para 2 dimensões (87% da variância preservada)
- **Clusters identificados:**
  - Cluster 0 — aeroportos médios com atrasos imprevisíveis (desvio padrão de 46 min)
  - Cluster 1 — aeroportos pequenos e pontuais (atraso médio de 3,2 min)
  - Cluster 2 — grandes hubs (ATL, ORD, DFW) com atrasos frequentes mas previsíveis

---

## Principais Resultados

| Modelo | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| Regressão Logística | 0.61 | 0.26 | 0.63 | 0.37 |
| Random Forest | 0.57 | 0.26 | 0.70 | 0.38 |

O Random Forest foi escolhido como modelo final por apresentar maior Recall — métrica prioritária no contexto de previsão de atrasos.

---

## Limitações

- O modelo não considera dados climáticos, uma das principais causas de atraso
- Precision baixa (~26%), gerando falsos positivos
- Limiar de 15 minutos segue padrão DOT mas é arbitrário
- Aeroportos com código numérico foram removidos por impossibilidade de mapeamento

---

## Tecnologias Utilizadas

- Python 3
- Pandas, NumPy
- Matplotlib, Seaborn
- Scikit-learn (LogisticRegression, RandomForestClassifier, KMeans, PCA, StandardScaler)

---

## Autora

Maria Thereza Moss de Abreu
Pós Tech FIAP — Machine Learning Engineering​​​​​​​​​​​​​​​​
