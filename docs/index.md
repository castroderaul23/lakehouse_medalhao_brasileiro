# Trabalho 3 — Lakehouse no Databricks (Medalhão)

Este projeto implementa um pipeline no Databricks seguindo a arquitetura **Landing → Bronze → Silver → Gold**, com execução **encadeada via Job** e entrega de um **modelo dimensional (Kimball)** na camada Gold.

## Resultados (Gold)
- `gold.dim_data`
- `gold.dim_time`
- `gold.dim_estadio`
- `gold.fact_partida`