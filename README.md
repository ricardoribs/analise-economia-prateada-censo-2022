# 👴💰 Análise da Economia Prateada: Censo 2022

![Status](https://img.shields.io/badge/Status-Concluído-green)
![Python](https://img.shields.io/badge/Python-3.x-blue)
![Power BI](https://img.shields.io/badge/PowerBI-Desktop-yellow)

## 🎯 O Desafio
O Brasil está envelhecendo rapidamente. O objetivo deste projeto foi utilizar dados reais do **Censo Demográfico 2022 (IBGE)** para identificar oportunidades de negócios e políticas públicas voltadas para a **Economia Prateada** (população 60+).

O desafio consistiu em mapear "Hotspots": municípios com **alto índice de envelhecimento**, **alta renda** e **alta taxa de idosos morando sozinhos**.

---

## 📊 O Resultado (Dashboard)

![Visão Geral do Dashboard](https://github.com/ricardoribs/analise-economia-prateada-censo-2022/blob/main/dashboard_print.png.PNG?raw=true)

### Principais Insights
1.  **Matriz de Oportunidade:** Cruzamento entre *Renda Média* vs. *Isolamento*. Identificamos cidades onde os idosos possuem alto poder aquisitivo e moram sozinhos (público-alvo para serviços de Home Care e condomínios assistidos).
2.  **Top 10 Envelhecimento:** Ranking dos municípios onde a transição demográfica está mais avançada.
3.  **Geografia:** O mapa de calor revelou concentrações claras de oportunidades na região Sul e Sudeste.

---

## ⚙️ Engenharia de Dados (ETL)

Os dados do Censo 2022 não estavam prontos para análise. Foi necessário construir um pipeline de dados robusto utilizando **Python (Pandas)**.

### 1. Coleta de Dados (Fontes)
Os dados foram extraídos do SIDRA/IBGE e de microdados oficiais:
* **Tabela 9514:** População por Idade.
* **Tabela 9879:** Domicílios Unipessoais.
* **Tabela 10291:** Rendimento Nominal Mensal.

### 2. Transformação (Python)
O processo de limpeza envolveu:
* Limpeza de cabeçalhos complexos do IBGE.
* Tratamento de dados não numéricos e valores nulos.
* Criação de chaves de ligação (`Join Keys`) para unificar bases com nomes de municípios divergentes.
* **Cálculo de KPIs:** Índice de Envelhecimento e % Domicílios Unipessoais.

### 3. Carga (Output)
O resultado foi uma "Tabela Mestre" consolidada, pronta para ser consumida pelo Power BI.

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.10 (Pandas, NumPy)
* **Visualização:** Microsoft Power BI
* **Ambiente:** Google Colab

