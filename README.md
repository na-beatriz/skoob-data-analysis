# 📚 Projeto de Dados – Análise de Livros Brasileiros na Plataforma Skoob

## 🚀 Descrição

Projeto de pipeline de dados desenvolvido em Python, com o objetivo de extrair, transformar e analisar dados de livros cadastrados na plataforma **Skoob**, com foco nos gêneros **Suspense** e **Fantasia**. Este projeto simula um fluxo de dados estruturado, aplicando tratamento, enriquecimento e categorização, gerando relatórios específicos para análise de leitores e autores desses gêneros.

## 🎯 Objetivo do Projeto

* Ler o dataset de livros brasileiros extraído do Skoob.
* Realizar transformações nos dados para padronização e enriquecimento.
* Gerar dois relatórios segmentados:

  * 📑 **Autores** dos gêneros **Suspense** e **Fantasia**.
  * 📑 **Leitores** (comportamento de avaliação e popularidade) desses mesmos gêneros.

## 🛠️ Tecnologias e Ferramentas

* Python 3.11
* Pandas
* Seaborn (opcional, para análise visual)
* Matplotlib (opcional)
* JupyterLab (ambiente de desenvolvimento)

## 📦 Pipeline ETL

### 🔍 Extração (Extract)

* **Fonte:** Arquivo CSV localizado em:

```
data/raw/livros_skoob.csv  
```

* Leitura do dataset utilizando pandas:

```python
import pandas as pd  
df = pd.read_csv('data/raw/livros_skoob.csv')  
```

### 🔧 Transformação (Transform)

✅ **Padronização e Tratamento de Dados:**

* Renomeação de colunas para padrão snake\_case.
* Normalização de textos (remoção de acentuação, espaços, e padronização de maiúsculas/minúsculas).
* Tratamento de valores nulos e inconsistentes.

✅ **Criação da coluna `nivel_popularidade` com as seguintes regras:**

* Favoritos > 1000 → `'Alta'`
* Favoritos entre 500 e 1000 → `'Média'`
* Favoritos < 500 → `'Baixa'`

```python
def classificar_popularidade(favoritos):  
    if favoritos > 1000:  
        return 'Alta'  
    elif favoritos >= 500:  
        return 'Média'  
    else:  
        return 'Baixa'  

df['nivel_popularidade'] = df['num_favoritos'].apply(classificar_popularidade)  
```

✅ **Segmentação:**

* Filtro aplicado para selecionar livros dos gêneros **Suspense** e **Fantasia**.

✅ **Enriquecimento:**

* Geração de relatórios separados com foco em:

  * **Autores:** informações sobre popularidade e avaliação média dos livros.
  * **Leitores:** comportamento em termos de avaliações, resenhas e favoritos.

✅ **Ordenação:**

* Dados organizados do mais bem avaliado para o menos bem avaliado.

### 💾 Carga (Load)

* Dados processados exportados em:

```
data/refined/autores_susp_fant.csv  
data/refined/leitores_susp_fant.csv  
```

```python
df_autores.to_csv('data/refined/autores_susp_fant.csv', index=False)  
df_leitores.to_csv('data/refined/leitores_susp_fant.csv', index=False)  
```

## 📑 Estrutura de Diretórios

```
📁 etl_skoob_2024/  
├── 📁 data/                                     # Dados brutos e processados  
│   ├── 📁 raw/                                  # Dados brutos  
│   │   └── livros_skoob.csv                     # Dataset original (fonte)  
│   └── 📁 refined/                              # Dados tratados  
│       ├── autores_susp_fant.csv                # Dataset de autores (Suspense e Fantasia)  
│       └── leitores_susp_fant.csv               # Dataset de leitores (Suspense e Fantasia)  
├── 📁 script/                                   # Scripts de transformação  
│   └── 📁 refined/                              # Scripts da camada refined  
│       ├── refined_script.ipynb                 # Notebook de transformação refined  
│       └── trusted_script.ipynb                 # Notebook de validação/ajustes finais  
└── README.md                                    # Documentação do projeto  
```

## 🔗 Dependências

* pandas
* seaborn (opcional)
* matplotlib (opcional)

**Instalação:**

```bash
pip install pandas seaborn matplotlib  
```

## 📈 Resultados

* Dois arquivos CSV consolidados, segmentados pelos gêneros **Suspense** e **Fantasia**:

  * 📑 **autores\_susp\_fant.csv** → Dados sobre autores e seus livros, com métricas de avaliação e popularidade.
  * 📑 **leitores\_susp\_fant.csv** → Dados relacionados ao comportamento dos leitores (favoritos, avaliações e resenhas).
* Inclusão da coluna **nivel\_popularidade**, categorizando os livros em Alta, Média e Baixa popularidade.

## 🔍 Insights Possíveis

* Identificação dos autores mais populares e mais bem avaliados nos gêneros analisados.
* Análise de discrepâncias entre popularidade (favoritos) e avaliação (nota média).
* Detecção de oportunidades de mercado: autores ou livros muito bem avaliados, mas com baixa popularidade.
* Geração de recomendações para estratégias de marketing, curadoria e lançamentos.

## 🤝 Contribuição

Fique à vontade para abrir issues, propor melhorias, sugestões de novos filtros, KPIs adicionais ou otimizações nos scripts.

## 🏷️ Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo LICENSE para mais informações.
