# Northern Star Shop - Data Pipeline

ETL pipeline koji spaja podatke prodavnice (porudzbine, proizvodi) sa
podacima lige (timovi, utakmice) da odgovori na pitanje: da li pobede
timova uticu na prodaju opreme tog tima?

## Izvori podataka

- Porudzbine: API (JSON, paginacija, 38 strana)
- Proizvodi: CSV fajl iz sistema prodavnice
- Timovi: CSV fajl od lige
- Utakmice: Parquet fajl sa platforme lige

## Sta pipeline radi

1. Extract - preuzima sve 4 izvora (`extract`)
2. Clean - cisti proizvode i porudzbine (`clean_products`, `clean_orders`)
3. Validate/Split - izbacuje duplikate i neispravne redove (`split_orders`)
4. Transform - racuna ukupnu vrednost porudzbine, spaja sa proizvodima (`transform_orders`)
5. Rezultati utakmica - pretvara utakmice u rezultate po timu (`team_results`)
6. Tabela lige (`league_table`)
7. Prozori posle utakmica - 3 dana posle svake utakmice (`match_windows`)
8. Analiza prodaje posle rezultata (`sales_after_results`)
9. Load - upisuje sve rezultate u `data/processed/`

## Pokretanje

summary = run_pipeline(RAW_DIR, PROCESSED_DIR)
