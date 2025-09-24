# ✈️ Projeto: Análise e Previsão de **Load Factor** (ANAC)

Este repositório reúne um fluxo de **ETL + EDA + Modelagem** para analisar e projetar o **load factor** (taxa de ocupação de assentos) da aviação comercial brasileira a partir dos **microdados da ANAC**, cobrindo o período de **jan/2023 a jul/2025**.

> Arquivo principal do projeto: **`projeto_machine_learning_load_factor.ipynb`**

---

## 🎯 Objetivo

* Consolidar e limpar os microdados oficiais da ANAC.
* Calcular o **load factor diário/mensal** por companhia aérea e por recorte de negócio (ex.: REGULAR / DOMÉSTICA).
* Explorar padrões sazonais (por mês e por dia da semana) e tendências.
* Treinar modelos de **regressão** (Spark MLlib) para **prever o load factor** nos meses seguintes.
* Comparações entre empresas **AD (Azul), G3 (Gol) e JJ (Latam)**  

---

## 📊 Fonte dos Dados

Os dados utilizados são da base **Básica** disponibilizada pela ANAC:  
👉 [Microdados da Aviação Comercial - ANAC](https://www.gov.br/anac/pt-br/assuntos/regulados/empresas-aereas/Instrucoes-para-a-elaboracao-e-apresentacao-das-demonstracoes-contabeis/envio-de-informacoes/microdados)

- Período considerado: **janeiro/2023 até julho/2025**  
- Colunas utilizadas incluem:
  - Companhia aérea (`sg_empresa_iata`)
  - Tipo de voo (`ds_natureza_etapa`)
  - Grupo de voo (`ds_grupo_di`)
  - Número de passageiros pagos/grátis
  - Assentos ofertados
  - Tipo de serviço (excluindo cargueiro)


## 🛠️ Tecnologias Utilizadas

- **PySpark** → leitura, tratamento e transformação dos dados em larga escala  
- **Pandas** → integração e manipulação de subconjuntos de dados  
- **Matplotlib** → visualizações (séries temporais, gráficos comparativos)  
- **Python** (Jupyter Notebook)  

## 📂 Estrutura do Repositório
```
load_factor_anac/
│── projeto_machine_learning_load_factor.ipynb # Notebook principal com ETL e análises
│── data/ # (opcional) pasta para armazenamento local de arquivos
│── README.md # Este arquivo
│── requirements.txt
```

## ⚙️ Ambiente e requisitos

O notebook utiliza **PySpark** para engenharia de atributos e modelagem, além de bibliotecas Python usuais.

### Requisitos mínimos

* **Python 3.10+**
* **Java 11+** (necessário para PySpark)
* Bibliotecas: `pyspark`, `pandas`, `numpy`, `matplotlib`

### Exemplo de `requirements.txt`

```txt
pyspark>=3.5
pandas>=2.2
numpy>=1.26
matplotlib>=3.8
jupyter>=1.0  # opcional, para executar localmente
ipykernel>=6  # opcional, para registrar o kernel do projeto
```

### Configuração rápida (Linux/macOS)

```bash
# 1) Crie e ative um ambiente virtual
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 2) Instale as dependências
pip install -r requirements.txt

# 3) Garanta o Java instalado e exporte JAVA_HOME, se necessário
# Exemplo (ajuste conforme seu sistema):
export JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"

# 4) Rode o Jupyter e abra o notebook
jupyter notebook notebooks/projeto_machine_learning_load_factor.ipynb
```

> Caso utilize **VS Code**, instale a extensão **Jupyter** e selecione o kernel do ambiente virtual.

---


## 🧹 ETL (resumo)

1. **Leitura** dos CSV/ZIP dos microdados.
2. **Seleção de recortes** (ex.: `ds_grupo_di == "REGULAR"`, `ds_natureza_etapa == "DOMÉSTICA"`, empresas de interesse como `AD`, `G3`, `JJ`).
3. **Limpeza** (remoção de colunas vazias/irrelevantes, padronização de datas e tipos).
4. **Features**:

   * `load_factor_dia` por voo/data (razão entre passageiros e assentos ofertados).
   * Agregações **diárias** e **mensais** por companhia.

> Os passos estão implementados e comentados diretamente no notebook.

---

## 🔎 EDA (exploração)

* Evolução **mensal** do load factor por companhia.
* Comportamento **por dia da semana**.
* Identificação de sazonalidade e outliers.

Gráficos típicos:

* Linha: **Evolução mensal** do `load_factor` (ex.: `plt.plot` por companhia).
* Barras: **Distribuição por dia da semana**.

---

## 🤖 Modelagem (Spark MLlib)

Modelos de regressão utilizados no notebook:

* **LinearRegression**
* **RandomForestRegressor**
* **GBTRegressor**

Pipeline geral:

1. Montagem de vetores com **`VectorAssembler`**.
2. Treino/validação com **`RegressionEvaluator`**.
3. **Previsões** para a janela de interesse (ex.: próximos 3 meses) e comparação por companhia aérea.

> Ajuste hiperparâmetros, janelas e variáveis explicativas conforme sua necessidade.

---

## ▶️ Como executar o projeto

1. **Baixe** os microdados da ANAC e **coloque em `data/raw/`**.
2. **Execute** o notebook `notebooks/projeto_machine_learning_load_factor.ipynb` (ou na raiz, conforme seu layout) e siga as células na ordem.
3. **Salve** as saídas (tabelas/figuras) em `data/processed/` e `reports/figures/`, se desejar organizar resultados.

---

## 📈 Exemplos de resultados

* Curvas do **load factor mensal** por companhia (2023‑01 → 2025‑07).
* **Tabela/CSV** com previsões por data/companhia.
* Gráficos de **importância de features** nos modelos de árvore (quando aplicável).

> Os exemplos são gerados durante a execução do notebook e podem variar conforme o período/dados carregados.

---

## 📝 Notas e boas práticas

* **Datas faltantes**: verifique lacunas e trate-as antes de treinar modelos.
* **Qualidade dos dados**: cheque valores zerados (ex.: passageiros pagos/grátis) e registros de carga quando não deseja incluí-los.
* **Reprodutibilidade**: fixe seeds quando comparar modelos.

---

## 📚 Créditos

* **Dados**: Agência Nacional de Aviação Civil (ANAC) – microdados públicos.
* **Projeto e estudo**: este repositório foi criado para estudo/aprendizado em ciência de dados e engenharia de dados com foco em séries temporais/ML para **load factor**.

---



## 💬 Contato

Sinta-se à vontade para abrir **Issues** ou **Pull Requests** com sugestões de melhoria, correções e novas análises.

