# Arquitetura Medalhão

## Landing (CSV)
- Ingestão dos arquivos CSV armazenados em Volume.
- Criação das tabelas `landing.brasileirao`, `landing.times`, `landing.estadio`.

## Bronze (Delta)
- Conversão das tabelas do Landing para Delta Lake:
- `bronze.brasileirao`, `bronze.times`, `bronze.estadio`.

## Silver (Data Quality)
- Aplicação de DQ somente em `silver.brasileirao`:
  - Padronização dos nomes de times em `time_mandante` e `time_visitante`
  - Remoção de sufixos `-FC/-SC/-EC` e também `FC/SC/EC`
  - Correção `Atlético-PR` → `Athletico-PR`
- `silver.times` e `silver.estadio` sem transformações.

## Gold (Kimball)
- Construção do Star Schema:
  - Dimensões: `dim_data`, `dim_time`, `dim_estadio`
  - Fato: `fact_partida`