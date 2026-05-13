# Trabalho 3 — Lakehouse no Databricks (Free Edition) + Arquitetura Medalhão

## 🎯 Objetivo
Construir um pipeline de dados no Databricks aplicando a arquitetura medalhão **Landing → Bronze → Silver → Gold**, com execução **encadeada via Job (Workflows)** e modelagem dimensional (Kimball) na camada Gold.

---

## 🧾 Dataset (CSV)
Tabelas utilizadas:
- **brasileirao.csv**: partidas com métricas do jogo (tabela base)
- **times.csv**: dimensão de times (`time`, `apelido`)
- **estadio.csv**: dimensão de estádios (`estadio`, `cidade`, `capacidade_maxima`)

Os arquivos foram carregados em um **Unity Catalog Volume** no Databricks Free Edition.

---

## 🏗️ Arquitetura Medalhão (Camadas)

### Landing (CSV)
- Ingestão dos CSVs e criação das tabelas no schema `landing`.

### Bronze (Delta)
- Conversão das tabelas do Landing para **Delta Lake** no schema `bronze`.

### Silver (Data Quality)
- Aplicação de regras de qualidade de dados **somente** em `silver.brasileirao`:
  - Padronização em `time_mandante` e `time_visitante` removendo `-FC/-SC/-EC` e também `FC/SC/EC`
  - Correção: `Atlético-PR` → `Athletico-PR`
- `silver.times` e `silver.estadio` seguem sem transformações.

### Gold (Kimball / Star Schema)
Criação das tabelas no schema `gold`:
- `gold.dim_data`
- `gold.dim_time`
- `gold.dim_estadio`
- `gold.fact_partida`

---

## 🔁 Orquestração (Job)
O pipeline é executado por um **Databricks Job** com tasks em sequência:
1. `01_landing_ingest`
2. `02_bronze_delta`
3. `03_silver_dq`
4. `04_gold_kimball`

Esse encadeamento é visualizado no **DAG** do Job (grafo de dependências entre tasks).

**Nome do Job:** (preencha aqui com o nome exato do seu Job no Databricks)

---

## ▶️ Como executar (passo a passo curto)
1. Fazer upload dos CSVs no Volume do Unity Catalog.
2. Rodar o Job em **Jobs & Pipelines**.
3. Validar as tabelas na camada Gold (`gold.*`).

---

## 📸 Evidências (prints)
Os prints usados na documentação estão em: `docs/assets/img/`

- DAG do Job: `docs/assets/img/job_dag.png`
- Execução do Job (Run Succeeded): `docs/assets/img/job_run_success.png`
- Star Schema (Gold): `docs/assets/img/star_schema.png`
- Validação Gold (ex.: COUNT na fato): `docs/assets/img/gold_fact_count.png`

---

## 📚 Documentação completa (MkDocs)
A documentação detalhada está em `docs/` (MkDocs), incluindo:
- Arquitetura medalhão
- Pipeline por notebook
- Star Schema (Kimball)
- Evidências do Job

### 🌐 Site público (GitHub Pages)
📌 **Link:** 
https://castroderaul23.github.io/lakehouse_medalhao_brasileiro/