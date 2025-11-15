# 📊 Pipeline de Dados – Censo 2022: Economia Prateada

[![Python](https://img.shields.io/badge/python-3.10-blue?logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/pandas-1.6.2-brightgreen?logo=pandas)](https://pandas.pydata.org/)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github)](https://github.com/seuusuario/censo60plus-analytics)

## 🔹 Objetivo
Construir um **conjunto de dados mestre** (uma tabela única) para alimentar um **dashboard analítico**, cruzando dados **demográficos, socioeconômicos e de infraestrutura de moradia**.  
O foco é identificar tendências de **envelhecimento populacional** (Economia Prateada) em nível municipal.  

---

## 🔹 Estrutura do Projeto

**📁 Pasta Principal:** `Projeto_Censo_Economia_Prateada`  
**🌐 Repositório Git:** `censo60plus-analytics`  

**Subpastas:**  
- `01_Dados_Brutos/` – Armazenamento dos 15 arquivos `.xlsx` baixados do IBGE.  
- `02_Dados_Tratados/` – Destino do arquivo CSV mestre.  
- `03_Dashboard/` – Dashboard final (visualização e análise).  

---

## 🔹 Coleta de Dados (Extract)

Foram coletadas **10 fontes de dados principais**, totalizando **15 arquivos físicos**.

| Item do Projeto | Fonte (IBGE) | Tabela | Arquivo(s) |
|-----------------|--------------|--------|------------|
| 👶 Idade (Pirâmide, IE) | Censo 2022 | 9514 | `01_Idade_Municipios.xlsx` |
| 🏠 Domicílios (Unipessoal, 60+) | Censo 2022 | 9879 | `02_Domicilios_Municipios.xlsx` |
| 💰 Renda (por Idade/Raça) | Censo 2022 | 10291 | `03_Renda_Municipios.xlsx` |
| 💍 Estado Civil | Censo 2022 | 10185 | `04_EstadoCivil_Municipios.xlsx` |
| 🎓 Escolaridade | Censo 2022 | 10061 | `05_A-Branca.xlsx` até `05_F.xlsx` |
| 🌆 Situação (Urbano/Rural) | Censo 2022 | 9922 | `06_Situacao_Domicilio.xlsx` |
| 🚰 Saneamento (Água) | Censo 2022 | 6803 | `08_Saneamento_Agua.xlsx` |
| 💩 Saneamento (Lixo) | Censo 2022 | 6892 | `09_Saneamento_Lixo.xlsx` |
| 🚽 Saneamento (Esgoto) | Censo 2022 | 6805 | `07_Saneamento_Esgoto.xlsx` |
| 🏗 Tipo de Construção | Censo 2022 | 9928 | `10_Moradia_Construcao.xlsx` |

---

## 🔹 Limpeza e Transformação (Python / Google Colab)

Notebook principal: [`Limpeza_Censo_2022.ipynb`](02_Dados_Tratados/Limpeza_Censo_2022.ipynb)

**⚡ Desafios superados:**  
- 🗂 **Cabeçalhos MultiIndex:** Resolvido com a função `flatten_ibge_cols` e `header=[...]`.  
- 🔄 **Dados pivotados/misturados:** Usado `.ffill()` para preencher municípios e raças.  
- 🗑 **Linhas de lixo (Totais de Estado):** Removidas via `.drop(0)` e lógica de `.ffill()`.  
- ❌ **Duplicação de municípios (Arquivo 2):** Resolvido com `.groupby().agg()` e `.drop_duplicates()`, garantindo 1 linha por município.  

**📌 DataFrames tratados:** `df_final_idade`, `df_final_domicilios`, `df_final_renda`, etc.  

---

## 🔹 Junção Final (Merge)

**🔧 Procedimentos aplicados:**  
1. 🏷 **Criação da chave:** `Chave_Municipio` padronizada em todas as tabelas (removendo `(UF)`).  
2. 📊 **Agregação:** Tabelas de Renda, Estado Civil e Escolaridade agregadas para manter apenas dados de "Total".  
3. ✅ **Correção de duplicatas:** Duplicatas removidas da tabela base (`df_final_idade`) antes do merge.  
4. 🏷 **Sufixos exclusivos:** Cada merge executado com `suffixes=('', '_Renda')` (ou similar) para evitar colisão de nomes.  
5. 🔗 **Resultado:** Merge `how='left'` bem-sucedido, gerando um DataFrame final com **5.316 municípios**.  

---

## 🔹 Resultado Final (Output)

- **📂 DataFrame mestre:** `df_dashboard`  
- **📊 Número de colunas:** 189  
- **💾 Exportação:** CSV final salvo em `02_Dados_Tratados/04_DADOS_MESTRES_CENSO_2022_v2.csv`  

---

## 🔹 Observação Final

💡 Toda a **limpeza e integração** foram realizadas **manual e programaticamente com scripts robustos**, garantindo **reprodutibilidade e consistência** — requisito essencial para análises em escala municipal.  

---

## 🔹 Como Usar

1. Clone o repositório:  
```bash
git clone https://github.com/seuusuario/censo60plus-analytics.git
