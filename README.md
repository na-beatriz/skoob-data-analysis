Projeto de Dados – Análise de Livros Brasileiros na Plataforma Skoob

🚀 Descrição

Este projeto de pipeline de dados, desenvolvido em Python, tem como objetivo extrair, transformar e analisar dados de livros cadastrados na plataforma Skoob, com foco nos gêneros Suspense e Fantasia. Ele simula um fluxo de dados estruturado, aplicando tratamento, enriquecimento e categorização, gerando relatórios específicos para análise de leitores e autores desses gêneros.

🎯 Objetivo do Projeto

  * Ler o dataset de livros brasileiros extraído do Skoob.
  * Realizar transformações nos dados para padronização e enriquecimento.
  * Gerar dois relatórios segmentados:
      * 📑 Autores dos gêneros Suspense e Fantasia.
      * 📑 Leitores (comportamento de avaliação e popularidade) desses mesmos gêneros.

🛠️ Tecnologias e Ferramentas

  * Python 3.11
  * Pandas
  * Seaborn (opcional, para análise visual)
  * Matplotlib (opcional)
  * JupyterLab (ambiente de desenvolvimento)

📦 Pipeline ETL

🔍 Extração (Extract)

  * **Fonte:** Arquivo CSV localizado em:
    `data/raw/livros_skoob.csv`
  * **Leitura do dataset utilizando pandas:**
    ```python
    import pandas as pd
    df = pd.read_csv('data/raw/livros_skoob.csv')
    ```

🔧 Transformação (Transform)

  * ✅ **Padronização e Tratamento de Dados:**

      * Renomeação de colunas para padrão `snake_case`.
      * Normalização de textos (remoção de acentuação, espaços e padronização de maiúsculas/minúsculas).
      * Tratamento de valores nulos e inconsistentes.

  * ✅ **Criação da coluna `nivel_popularidade` com as seguintes regras:**

      * Favoritos \> 1000 → 'Alta'
      * Favoritos entre 500 e 1000 → 'Média'
      * Favoritos \< 500 → 'Baixa'

    <!-- end list -->

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

  * ✅ **Segmentação:**

      * Filtro aplicado para selecionar livros dos gêneros Suspense e Fantasia.

  * ✅ **Enriquecimento:**

      * Geração de relatórios separados com foco em:
          * **Autores:** informações sobre popularidade e avaliação média dos livros.
          * **Leitores:** comportamento em termos de avaliações, resenhas e favoritos.

  * ✅ **Ordenação:**

      * Dados organizados do mais bem avaliado para o menos bem avaliado.

💾 Carga (Load)

  * **Dados processados exportados em:**

      * `data/trusted/autores_susp_fant.csv`
      * `data/trusted/leitores_susp_fant.csv`
      * `data/trusted/livros_susp_fant.csv` (novo arquivo adicionado)

    <!-- end list -->

    ```python
    df_autores.to_csv('data/trusted/autores_susp_fant.csv', index=False)
    df_leitores.to_csv('data/trusted/leitores_susp_fant.csv', index=False)
    df_livros.to_csv('data/trusted/livros_susp_fant.csv', index=False) # Exemplo, se você gerou um df_livros
    ```

📑 Estrutura de Diretórios

```
📁 etl_skoob_2024/
├── 📁 data/                                     # Dados brutos e processados
│   ├── 📁 raw/                                  # Dados brutos
│   │   └── livros_skoob.csv                     # Dataset original (fonte)
│   └── 📁 trusted/                              # Dados tratados e validados (anteriormente 'refined')
│       ├── autores_susp_fant.csv                # Dataset de autores (Suspense e Fantasia)
│       ├── leitores_susp_fant.csv               # Dataset de leitores (Suspense e Fantasia)
│       └── livros_susp_fant.csv                 # Novo dataset de livros (Suspense e Fantasia)
├── 📁 img/                                      # Imagens e gráficos gerados
├── 📁 scripts/                                  # Scripts de transformação
│   ├── 📁 refined/                              # Scripts da camada refined
│   │   └── refined_script.ipynb                  # Notebook de transformação refined
│   └── 📁 trusted/                              # Scripts da camada trusted (validação/ajustes finais)
│       └── trusted_script.ipynb                 # Notebook de validação/ajustes finais
└── README.md                                    # Documentação do projeto
```

🔗 Dependências

  * pandas
  * seaborn (opcional)
  * matplotlib (opcional)

**Instalação:**

```bash
pip install pandas seaborn matplotlib
```

📈 Resultados

Três arquivos CSV consolidados, segmentados pelos gêneros Suspense e Fantasia:

  * 📑 `autores_susp_fant.csv` → Dados sobre autores e seus livros, com métricas de avaliação e popularidade.
  * 📑 `leitores_susp_fant.csv` → Dados relacionados ao comportamento dos leitores (favoritos, avaliações e resenhas).
  * 📑 `livros_susp_fant.csv` → Dados dos livros filtrados por Suspense e Fantasia, incluindo a nova coluna de popularidade.

Inclusão da coluna `nivel_popularidade`, categorizando os livros em Alta, Média e Baixa popularidade.

🔍 Insights Possíveis

  * Identificação dos autores mais populares e mais bem avaliados nos gêneros analisados.
  * Análise de discrepâncias entre popularidade (favoritos) e avaliação (nota média).
  * Detecção de oportunidades de mercado: autores ou livros muito bem avaliados, mas com baixa popularidade.
  * Geração de recomendações para estratégias de marketing, curadoria e lançamentos.

🤝 Contribuição

Fique à vontade para abrir issues, propor melhorias, sugestões de novos filtros, KPIs adicionais ou otimizações nos scripts.

🏷️ Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo LICENSE para mais informações.