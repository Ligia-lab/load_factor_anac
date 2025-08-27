# ✈️ Projeto de Análise do Load Factor - ANAC (2023–2025)

Este repositório apresenta um estudo sobre o **Load Factor (fator de aproveitamento dos assentos)** das principais companhias aéreas brasileiras, utilizando os **microdados públicos da ANAC**.

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

## 🎯 Objetivo

Explorar e calcular o **fator de aproveitamento de assentos (Load Factor)** das companhias aéreas:
- Evolução **mensal por companhia aérea**  
- Diferenças por **dia da semana**  
- Comparações entre empresas **AD (Azul), G3 (Gol) e JJ (Latam)**  

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
```


## 📈 Etapas da Análise

1. **Carregamento dos dados**  
   - Arquivos da ANAC (zipados) são extraídos e lidos no PySpark.  

2. **Tratamento de dados**  
   - Filtros aplicados:  
     - Companhias `AD`, `G3`, `JJ`  
     - Voos domésticos  
     - Grupo **REGULAR**  
   - Exclusão de serviços do tipo **CARGUEIRO**  
   - Tratamento de valores nulos e remoção de colunas irrelevantes  

3. **Cálculo de métricas**  
   - Cálculo do **Load Factor diário e mensal**  
   - Agrupamentos por **companhia** e por **dia da semana**  

4. **Visualizações**  
   - Evolução mensal do Load Factor por companhia aérea  
   - Comparação entre as principais empresas ao longo do tempo  

## 🚀 Como Executar

1. Clone este repositório:
   ```bash
   git clone https://github.com/Ligia-lab/load_factor_anac.git
   cd load_factor_anac
   ```
2. Instale as dependências:
   ```
   pip install -r requirements.txt
   ```
3. Abra o notebook no Jupyter:
   ```
   jupyter notebook projeto_machine_learning_load_factor.ipynb
   ```

   📌 Observações

- Os dados podem ser baixados diretamente do site da ANAC (link acima).

- O projeto foi desenvolvido em ambiente Google Colab, mas pode ser adaptado para execução local.

- Objetivo principal: estudo exploratório e educacional sobre a aplicação de PySpark em dados reais.

