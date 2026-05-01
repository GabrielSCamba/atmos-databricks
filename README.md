# atmos-databricks

Projeto de Engenharia de Dados utilizando Azure Databricks com arquitetura medalhão (Bronze, Silver e Gold) para ingestão, transformação e disponibilização de dados analíticos.

O projeto foi desenvolvido com base no curso disponibilizado pela Empregadados e tem como objetivo demonstrar a construção de pipelines modernos de dados utilizando recursos do ecossistema Databricks.

## Arquitetura

O projeto segue o padrão de arquitetura medalhão:

```text
Raw Data -> Bronze -> Silver -> Gold
```

### Bronze

Camada responsável pela ingestão dos dados brutos.

Principais responsabilidades:

* Leitura de arquivos de entrada
* Ingestão incremental com Auto Loader
* Persistência dos dados brutos
* Controle de schema
* Checkpoint de streaming
* Rastreabilidade da ingestão

### Silver

Camada responsável pelo tratamento e padronização dos dados.

Principais responsabilidades:

* Limpeza de dados
* Tratamento de valores nulos
* Padronização de colunas
* Conversão de tipos
* Regras de qualidade
* Enriquecimento de dados

### Gold

Camada analítica orientada ao negócio.

Principais responsabilidades:

* Agregações
* KPIs
* Modelagem analítica
* Tabelas para consumo em dashboards e análises

---

## Estrutura do Projeto

```text
atmos-databricks/
│
├── 01 - Create Bronze/
├── 02 - Create Silver/
├── 03 - Create Gold/
└── README.md
```

---

## Tecnologias Utilizadas

* Azure Databricks
* PySpark
* Delta Lake
* Databricks Auto Loader
* Structured Streaming
* Azure Data Lake Storage Gen2
* Unity Catalog

---

## Conceitos Aplicados

* Arquitetura Medalhão
* ETL/ELT
* Streaming de dados
* Data Lakehouse
* Governança de dados
* Evolução de schema
* Checkpoint e tolerância a falhas
* Observabilidade de pipelines

---

## Ingestão com Auto Loader

O projeto utiliza o Databricks Auto Loader para ingestão incremental de arquivos.

Exemplo:

```python
(
    spark.readStream
        .format("cloudFiles")
        .option("cloudFiles.format", "csv")
        .option("cloudFiles.schemaEvolutionMode", "addNewColumns")
)
```

Recursos utilizados:

* Descoberta automática de arquivos
* Evolução automática de schema
* Processamento incremental
* Checkpoint de streaming

---

## Organização das Camadas

### Bronze

Dados ingeridos sem transformações significativas.

Exemplo:

* Dados meteorológicos brutos
* Arquivos CSV originais
* Histórico completo

### Silver

Dados tratados e preparados.

Exemplo:

* Colunas padronizadas
* Tipagem corrigida
* Dados inconsistentes tratados

### Gold

Dados refinados para analytics.

Exemplo:

* Indicadores
* Métricas consolidadas
* Tabelas para BI

---

## Como Executar

### 1. Clone o repositório

```bash
git clone https://github.com/GabrielSCamba/atmos-databricks.git
```

### 2. Configure o ambiente no Databricks

Configure:

* Cluster
* Unity Catalog
* External Locations
* Storage Credential
* Volume ou caminho no ADLS Gen2

### 3. Execute os notebooks na ordem

1. Bronze
2. Silver
3. Gold

---

## Exemplo de Widget Utilizado

```python
dbutils.widgets.text("source_system", "", "Sistema de origem")
dbutils.widgets.text("source_path", "", "Diretório de entrada")
dbutils.widgets.text("target_table", "", "Tabela de destino")
```

Os widgets permitem parametrizar os pipelines e reutilizar os notebooks para múltiplas fontes.

---

## Possíveis Evoluções

* Integração com Azure Data Factory
* CI/CD com GitHub Actions
* Testes automatizados
* Monitoramento de pipelines
* Orquestração com Workflows
* Qualidade de dados com expectativas
* Deploy com Databricks Asset Bundles

---

## Objetivo do Projeto

Este projeto tem como objetivo consolidar conhecimentos em Engenharia de Dados utilizando Databricks e Azure, abordando desde ingestão até consumo analítico de dados.

---

## Autor

Gabriel Camba

* GitHub: [https://github.com/GabrielSCamba](https://github.com/GabrielSCamba)
* LinkedIn: [https://www.linkedin.com/](https://www.linkedin.com/)
