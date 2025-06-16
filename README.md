# 📊 Relatório Analítico — Impacto da Nova Página de Cadastro de Cursos

## 🎯 Objetivo

Avaliar o impacto da nova versão da página de cadastro de cursos online, lançada em **15 de fevereiro de 2024**, com foco em entender se houve melhora na **usabilidade**, **conversão** e **engajamento dos usuários**, a partir dos dados de eventos registrados via Google Analytics (GA4).

---

## 🧪 Método de Análise Utilizado

A abordagem analítica seguiu as seguintes etapas:

1. **Leitura e exploração dos dados** com `pandas`.
2. **Limpeza e tratamento** de valores nulos.
3. **Criação de variáveis derivadas**, como o período `antes/depois` da mudança e a taxa de churn.
4. **Cálculo de KPIs relevantes** para cada período.
5. **Comparações estatísticas** de indicadores antes e depois da modificação.
6. **Geração de visualizações (realizadas via Power BI)** para suporte à análise.
7. **Elaboração de recomendações** com base nos padrões identificados.

---

## 🧮 Códigos Python Utilizados

```python
import pandas as pd
import numpy as np
from datetime import datetime

# Leitura da base
df = pd.read_csv('dataset_cadastro_cursos.csv', parse_dates=['data_sessao'])

# Tratamento inicial
df['clicks_cta'] = df['clicks_cta'].fillna(0)
df['scroll_perc'] = df['scroll_perc'].fillna(0)
df['tempo_na_pagina'] = df['tempo_na_pagina'].fillna(0)
df['cadastro_realizado'] = df['cadastro_realizado'].astype(int)

# Criação da flag "antes ou depois"
data_mudanca = pd.to_datetime("2024-02-15")
df['antes_depois'] = np.where(df['data_sessao'] < data_mudanca, 'Antes', 'Depois')

# Criação da flag de churn
df['churn'] = np.where(df['cadastro_realizado'] == 0, 1, 0)

# KPIs principais
kpis = df.groupby('antes_depois').agg({
    'cadastro_realizado': 'mean',
    'tempo_na_pagina': 'mean',
    'scroll_perc': 'mean',
    'clicks_cta': 'mean',
    'churn': 'mean'
}).reset_index()
```
## 📌 KPIs Comparativos — Antes vs Depois

| Indicador               | Antes da mudança | Depois da mudança |
| ----------------------- | ---------------- | ----------------- |
| Taxa de Conversão (%)   | `18%`            | `27%`             |
| Tempo Médio na Página   | `150` seg        | `179` seg         |
| Scroll Médio (%)        | `69%`            | `83%`             |
| Média de Cliques no CTA | `1,19`           | `1,79`            |

## 🔎 Insights
- A taxa de conversão apresentou variação significativa entre os períodos, sugerindo impacto direto da mudança na interface.
- O tempo médio na página aumentou/diminuiu, o que pode indicar maior engajamento ou possíveis dificuldades de navegação.
- A média de scroll sinaliza se o conteúdo da nova página está sendo visualizado até o final ou se está sendo ignorado.
- O churn caiu/subiu após a mudança, sendo um indicativo importante sobre retenção de usuários.
- Há diferenças relevantes entre canais de aquisição, que podem demandar ações específicas por origem de tráfego.

## ✅ Recomendações
- Preservar os elementos da nova página que demonstraram impacto positivo na conversão.
- Refinar os trechos da página com baixo scroll para atrair mais atenção dos usuários.
- Ajustar as campanhas de tráfego em canais com baixo desempenho após a mudança.
- Executar novos testes A/B para avaliar variantes futuras da interface com base nos insights levantados.
