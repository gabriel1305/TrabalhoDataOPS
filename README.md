# 📦 Projeto DataOps - Comércio Exterior

Este projeto tem como objetivo automatizar o processo de **extração, transformação, carga e consumo (ETL)** de dados públicos de **importação e exportação** do comércio exterior brasileiro, utilizando o banco de dados **SQLite**. Os dados são estruturados em tabelas dimensionais e fatos para facilitar análises e consultas otimizadas.

---

## 🧱 Estrutura do Projeto

O projeto está organizado em notebooks Jupyter, cada um representando uma etapa do pipeline de dados:

- `extract.ipynb`: Responsável pela extração dos dados brutos.
- `transform.ipynb`: Realiza a transformação e limpeza dos dados extraídos.
- `ingest.ipynb`: Carrega os dados transformados no banco de dados SQLite.
- `consumer.ipynb`: Executa consultas analíticas sobre os dados carregados.
- `orquestration.ipynb`: Orquestra as etapas anteriores, garantindo a execução sequencial do pipeline.

---

## 💾 Banco de Dados

- Banco utilizado: **SQLite**
- Tabelas criadas:
  - `d_products_comex` — Tabela dimensional de produtos NCM.
  - `f_import_comex` — Tabela fato de importações.
  - `f_export_comex` — Tabela fato de exportações.

---

## 🔍 Consultas de Análise

Exemplo de consulta utilizada para obter **ranking mensal por estado (UF)** baseado no valor FOB:

```sql
SELECT 
    CO_ANO, 
    CO_MES, 
    SG_UF_NCM, 
    SUM(VL_FOB) AS Total_VL_FOB
FROM 
    f_import_comex
GROUP BY 
    CO_ANO, CO_MES, SG_UF_NCM
ORDER BY 
    CO_ANO DESC, CO_MES DESC, Total_VL_FOB DESC;
