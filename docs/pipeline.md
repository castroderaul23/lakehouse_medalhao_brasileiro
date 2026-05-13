# Pipeline (Notebooks)

## 01_landing_ingest
Lê CSVs do volume e grava `landing.*`.

## 02_bronze_delta
Lê `landing.*` e grava `bronze.*` em Delta.

## 03_silver_dq
Aplica Data Quality somente em `brasileirao` (times mandante/visitante) e grava `silver.*`.

## 04_gold_kimball
Cria dimensões e fato no schema `gold` (Kimball / Star Schema).