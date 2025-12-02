# 👴💰 Análise da Economia Prateada: Censo 2022

![Status](https://img.shields.io/badge/Status-Concluído-green)
![Python](https://img.shields.io/badge/Python-3.10-blue)
![Power BI](https://img.shields.io/badge/PowerBI-Desktop-yellow)
![Data Engineering](https://img.shields.io/badge/Focus-Data%20Engineering-orange)

## 🎯 O Desafio
O Brasil está passando por uma rápida transição demográfica. O objetivo deste projeto foi utilizar dados reais do **Censo Demográfico 2022 (IBGE)** para identificar oportunidades de negócios e políticas públicas voltadas para a **Economia Prateada** (população 60+).

O desafio consistiu em mapear "Hotspots": municípios com **alto índice de envelhecimento**, **alta renda** e **alta taxa de idosos morando sozinhos**.

---

## 📊 O Resultado (Dashboard)

![Visão Geral do Dashboard](https://github.com/ricardoribs/analise-economia-prateada-censo-2022/blob/main/dashboard_print.png.PNG?raw=true)

### Principais Insights
1.  **Matriz de Oportunidade Silver:** Cruzamento estratégico entre *Renda Média* vs. *Isolamento Domiciliar*. Identificamos cidades onde os idosos possuem alto poder aquisitivo e moram sozinhos (público-alvo ideal para serviços de Home Care e condomínios assistidos).
2.  **Top 10 Envelhecimento:** Ranking dos municípios onde a transição demográfica está mais avançada, liderados majoritariamente por cidades do Rio Grande do Sul.
3.  **Geografia:** O mapa de calor revelou concentrações claras de oportunidades nas regiões Sul e Sudeste.

---

## 📂 Estrutura do Projeto

```text
/
├── 📁 dados/               # Arquivos brutos (XLSX) e tratados (CSV)
├── 📁 notebooks/           # Jupyter Notebook com o código ETL (Google Colab)
├── 📁 dashboard/           # Arquivo .pbix do Power BI
├── 📁 imagens/             # Assets para documentação
└── README.md               # Documentação do projeto

🔄 Pipeline de Dados
O fluxo de Engenharia de Dados foi desenhado para transformar dados brutos e desconexos em inteligência de negócio:
graph LR
    A[SIDRA / IBGE] -->|Coleta Manual/XLSX| B(Google Colab / Python)
    B -->|Limpeza & Transformação| C{Pandas Dataframe}
    C -->|Cálculo de KPIs| D[Arquivo CSV Mestre]
    D -->|Importação| E[Power BI Desktop]
    E -->|Visualização| F[Dashboard Interativo]
1. Extração (Extract)
Os dados foram extraídos de microdados oficiais do IBGE:

◾ Tabela 9514: População por Idade.

◾ Tabela 9879: Domicílios Unipessoais.

◾ Tabela 10291: Rendimento Nominal Mensal (focado em 60+).
2. Transformação (Transform)
Utilizando Python (Pandas), o processo envolveu:

◾ Limpeza de cabeçalhos complexos ("lixo") dos arquivos do SIDRA.

◾ Tratamento de tipos de dados (conversão de texto para numérico e substituição de nulos).

◾ Engenharia de Atributos: Criação dos KPIs Índice de Envelhecimento e % Domicílios Unipessoais.
3. Carga (Load)
O resultado foi uma "Tabela Mestre" consolidada (04_DADOS_MESTRES_CENSO_2022_v2.csv), otimizada para performance no Power BI.

💻 Destaque Técnico (Python)
Um dos maiores desafios foi unificar bases com padrões de nomes divergentes (ex: "São Paulo" vs "São Paulo (SP)"). Solucionei criando uma chave de ligação limpa antes do Join:
# Criando uma chave única para o Join (Removendo a UF do nome)
df_final_idade['Chave_Municipio'] = df_final_idade['Município'].str.split(' \(').str[0].str.strip()

# Realizando o Merge das bases (Idade + Domicílios + Renda)
df_dashboard = pd.merge(
    df_final_idade,
    df_final_domicilios,
    on='Chave_Municipio',
    how='inner'
)
🚀 Próximos Passos & Melhorias
Este projeto é um MVP (Produto Mínimo Viável). Evoluções futuras incluem:
◾ Automação: Criar um script Python para buscar dados diretamente da API do SIDRA, eliminando o download manual.

◾ Cloud: Armazenar os dados tratados em um banco SQL na nuvem (AWS RDS ou Azure SQL).

◾ Novos Indicadores: Cruzar com dados do DATASUS para analisar a cobertura de saúde nessas cidades envelhecidas.
