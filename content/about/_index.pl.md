+++
title = "O mnie"
description = "Podsumowanie zawodowe, najważniejsze doświadczenia i kompetencje."
layout = "single"
+++

## Profil

Jestem Inżynierem Danych w Sollers Consulting. Na co dzień pracuję przy platformach danych w chmurze, pipeline'ach ETL/ELT oraz obszarze data quality.
Jestem otwarty na współpracę przy projektach związanych z danymi w firmach, szczególnie w obszarze projektowania, wdrażania oraz audytów systemów danych.

## Kluczowe kompetencje

- **Data engineering:** Snowflake, dbt, Fivetran, pipeline'y ETL/ELT, modelowanie i walidacja danych
- **Programowanie i analiza:** SQL, Python, R, PySpark
- **Chmura i infrastruktura:** AWS (S3), GitHub Actions, Azure (DevOps, Synapse, AI Foundry), Docker, Linux
- **Bazy danych:** PostgreSQL, DuckDB, MSSQL

## Wybrane osiągnięcia

### Budowa Common Data Model dla wiodącego London Market brokera

- Implementacja modeli dbt/Snowflake dla wspólnego modelu danych budowanego na bazie wielu podobnych źródeł klienckich.
- Projekt i wdrożenie CI/CD w dbt Cloud (DEV/STG/PROD), wraz ze standardami nazewnictwa, strukturą projektu i kontrolą jakości przed merge.
- Aktywna współpraca z architektami i klientem przy doprecyzowaniu wymagań oraz decyzjach pod skalowalność modelu pod kolejne typy źródeł danych.
- Onboarding nowych członków zespołu, przygotowanie dokumentacji wejściowej oraz code review i feedback wspierający utrzymanie jakości dostarczanych modeli.

### Migracja On-prem Reporting System do Chmury dla wiodącego London Market insurera

- Reverse-engineering logiki transformacji z Java do SQL i implementacja procedur transformacyjnych w Snowflake dla warstwy raportowej.
- Usprawnianie pipeline'ów ingestion i transformacji (Fivetran + Snowflake + S3/CDC), w tym optymalizacje pod odświeżanie przyrostowe.
- Skrypt w Pythonie (`multiprocessing`, `pandas`) do równoległego przetwarzania plików Parquet z S3 i ładowania do stagingu; skrócenie czasu ingestion z ok. 4h do ok. 45 min.
- Wsparcie rekonsyliacji danych między Snowflake a źródłem oraz wdrożenie stabilnego procesu historyzacji danych; finalnie odświeżanie całości raportingu co 15 minut zamiast raz dziennie.

## Wykształcenie

- **Inżynier (B.Eng.), Data Engineering and Analytics - Politechnika Lubelska**

## Linki

- [GitHub](https://github.com/TokarskiPatryk)
- [LinkedIn](https://www.linkedin.com/in/patryk-tokarski/)