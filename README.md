
---

## 📚 Fontes de Dados
| Item | Fonte (IBGE) | Arquivo |
|------|--------------|---------|
| 👵 Idade (Pirâmide) | Censo 2022 | 951401_...Idade_Municipios.xlsx |
| 🏠 Domicílios (Unipessoal, 60+) | Censo 2022 | 987902_...Domicilios_Municipios.xlsx |
| 💰 Renda (por Idade/Raça) | Censo 2022 | 1029103_...Renda_Municipios.xlsx |
| 💍 Estado Civil | Censo 2022 | 1018504_...EstadoCivil_Municipios.xlsx |
| 🎓 Escolaridade | Censo 2022 | 1006105_A_...Branca.xlsx (e mais 5 arquivos B-F) |
| 🌆 Situação (Urbano/Rural) | Censo 2022 | 992206_...Situacao_Domicilio.xlsx |
| 🚰 Saneamento (Esgoto/Água/Lixo) | Censo 2022 | 680507_...Saneamento_Esgoto.xlsx / 680308_...Saneamento_Agua.xlsx / 689209_...Saneamento_Lixo.xlsx |
| 🏗 Tipo de Construção | Censo 2022 | 992810_...Moradia_Construcao.xlsx |

---

## 🛠 Pipeline ETL

### 1️⃣ Limpeza e Transformação (Python/Colab)
- 🔹 Tratamento de cabeçalhos múltiplos (`MultiIndex`)  
- 🔹 Preenchimento de dados faltantes com `.ffill()`  
- 🔹 Remoção de linhas lixo (totais de estado)  
- 🔹 Correção de duplicatas por município com `.groupby().agg()` e `.drop_duplicates()`  

### 2️⃣ Junção Final (Merge)
- 🔹 Criação de chave única `Chave_Municipio`  
- 🔹 Agregação de tabelas com múltiplas linhas por município  
- 🔹 Merge left com sufixos únicos (`suffixes=('', '_Renda')`, etc.)  

### 3️⃣ Resultado
- 🔹 DataFrame final: `df_dashboard`  
- 🔹 **5.316 municípios**  
- 🔹 **189 colunas**  
- 🔹 Salvo em: `02_Dados_Tratados/04_DADOS_MESTRES_CENSO_2022_v2.csv`  

---

## 🚀 Como Usar

1. Clone o repositório via SSH:

```bash
git clone git@github.com:ETL4Good/censo60plus-analyticss.git

2. Entre na pasta do projeto:
cd censo60plus-analyticss

3. Abra o notebook Limpeza_Censo_2022.ipynb no Jupyter / Colab para rodar o pipeline de ETL.

4. Atualizar o repositório local:
git pull

5. Para enviar alterações para o GitHub:
git add .
git commit -m "Mensagem de commit"
git push
