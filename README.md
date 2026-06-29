# microdados_enem

Análise exploratória dos microdados do ENEM das edições de **2020 a 2023** usando PySpark.
O pipeline ETL e todas as análises estão consolidados em um único notebook (`enem_analise.ipynb`) que opera inteiramente em memória — nenhum dado intermediário é gravado em disco.

---

## Estrutura do repositório

```
microdados_enem/
├── enem_analise.ipynb      # notebook único: ETL + análises
├── roteiro.md              # dicionário de variáveis dos microdados brutos (INEP)
├── MICRODADOS_ENEM/        # arquivos-fonte em Parquet (não versionados)
│   ├── MICRODADOS_ENEM_2020.parquet
│   ├── MICRODADOS_ENEM_2021.parquet
│   ├── MICRODADOS_ENEM_2022.parquet
│   └── MICRODADOS_ENEM_2023.parquet
```

---

## Modelo de dados (star schema em memória)

O pipeline constrói seis DataFrames Spark que formam um star schema usado diretamente pelas análises:

| Tabela | Linhas aprox. | Descrição |
|---|---|---|
| `DIM_TEMPO` | 4 | Uma linha por edição; flag pós-pandemia |
| `DIM_RENDA` | 15 | Faixas de renda familiar do questionário socioeconômico (Q006) |
| `DIM_CANDIDATO` | ~900 | Perfis demográficos únicos (sexo × raça/cor × faixa etária × segmento). |
| `DIM_ESCOLA` | ~20 | Combinações únicas de tipo, dependência administrativa e localização |
| `DIM_LOCALIDADE` | ~1.500 | Municípios de aplicação da prova |
| `FATO_DESEMPENHO` | ~16 M | Uma linha por inscrito/ano; notas, presenças e chaves substitutas |

---

## Etapas do notebook

1. **Configuração** — SparkSession, imports e constantes de mapeamento
2. **Dimensões de suporte** — `DIM_TEMPO` e `DIM_RENDA` criadas diretamente em Python
3. **Carregamento e transformação** — leitura dos Parquets, cast de notas, flags de presença, médias, mapeamentos de raça/cor/escola/segmento
4. **Tabelas dimensionais** — `DIM_CANDIDATO`, `DIM_ESCOLA`, `DIM_LOCALIDADE`
5. **Tabela fato** — `FATO_DESEMPENHO` com resolução de todas as chaves substitutas
6. **Análises exploratórias** — cinco análises com visualizações Matplotlib/Seaborn

---

## Análises incluídas

| # | Análise |
|---|---|
| 6.1 | Taxa de abstenção total por ano |
| 6.2 | Gap de desempenho: escola pública vs privada por área |
| 6.3 | Desempenho por segmento: Treineiros, Concluintes e Egressos |
| 6.4 | Evolução do perfil racial dos inscritos e nota média |
| 6.5 | Impacto da renda familiar na nota média geral |

---

## Requisitos

```
pyspark>=4.0
matplotlib
seaborn
numpy
pyarrow       # leitura dos Parquets pelo Pandas (.toPandas())
```

---

## Como executar

Abra `enem_analise.ipynb` e execute as células em ordem.
Os arquivos Parquet devem estar em `MICRODADOS_ENEM/` relativo ao diretório do notebook.
