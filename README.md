# 📊 Relatório Analítico — Impacto da Nova Página de Cadastro de Cursos

## 🎯 Objetivo

Avaliar o impacto da nova versão da página de cadastro de cursos online, lançada em **15 de fevereiro de 2024**, com foco em entender se houve melhora na **usabilidade**, **conversão** e **engajamento dos usuários**, a partir dos dados de eventos registrados via Google Analytics (GA4).

---

## 🧪 Método de Análise Utilizado

A abordagem analítica seguiu as seguintes etapas:

1. **Leitura e exploração dos dados** com `pandas`.
2. **Criação de variáveis derivadas**, como o período `antes/depois` da mudança e a taxa de churn.
3. **Cálculo de KPIs relevantes** para cada período.
4. **Comparações estatísticas** de indicadores antes e depois da modificação.
5. **Geração de visualizações (realizadas via Power BI)** para suporte à análise.
6. **Elaboração de recomendações** com base nos padrões identificados.

---

## 🧮 Códigos Python Utilizados

```python
import pandas as pd
import numpy as np
from datetime import datetime

# Leitura da base
df = pd.read_csv('dataset_cadastro_cursos.csv', parse_dates=['data_sessao'])

# Criação da flag "antes ou depois"
data_mudanca = pd.to_datetime("2024-02-15")
df['antes_depois'] = np.where(df['data_sessao'] < data_mudanca, 'Antes', 'Depois')

# KPIs principais
kpis = df.groupby('antes_depois').agg({
    'cadastro_realizado': 'mean',
    'tempo_na_pagina': 'mean',
    'scroll_perc': 'mean',
    'clicks_cta': 'mean'
}).reset_index()
```
💡Acessar o arquivo 'exploratoria.ipynb' no caminho a seguir para acompanhar a análise detalhada.

├── desafio_yduqs
    ├── data
        ├── dataset_cadastro_cursos.csv
    ├── README.md
    ├── dashboard-mudanca-cadastro.pbix
    └── exploratoria.ipynb


## 📌 KPIs Comparativos — Antes vs Depois

| Indicador               | Antes da mudança | Depois da mudança |
| ----------------------- | ---------------- | ----------------- |
| Taxa de Conversão (%)   | `18%`            | `27%`             |
| Tempo Médio na Página   | `150` seg        | `179` seg         |
| Scroll Médio (%)        | `69%`            | `83%`             |
| Média de Cliques no CTA | `1,19`           | `1,79`            |

🔎 Insights
- A taxa de conversão aumentou significativamente de 18% para 27%, evidenciando que a nova página está mais eficaz em converter visitantes em cadastros.
- O tempo médio na página subiu de 150s para 179s, sugerindo que os usuários estão mais engajados ou encontrando mais conteúdo de interesse.
- O scroll médio cresceu de 69% para 83%, indicando que a nova estrutura visual incentiva a navegação completa da página.
- A média de cliques no botão de CTA subiu de 1,19 para 1,79, o que demonstra que os elementos de chamada para ação estão mais visíveis ou mais persuasivos.

✅ Recomendações
- Manter o novo design da página, já que os indicadores mostram melhora clara na jornada do usuário e nas conversões.
- Analisar elementos que contribuíram para o maior engajamento, como distribuição de informações, design do CTA ou organização do conteúdo.
- Monitorar a evolução contínua desses indicadores, garantindo que o desempenho se mantenha nos próximos meses.
- Estender esse modelo de interface para outras páginas críticas, testando se os mesmos ganhos de performance podem ser replicados.
- Realizar testes A/B periódicos, focando em variações de layout, texto ou posicionamento de CTA, para continuar otimizando a performance.
