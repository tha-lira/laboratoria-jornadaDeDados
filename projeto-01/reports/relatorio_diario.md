# Relatório Diário - Projeto de Análise de Dados – O Mercado


## Atividades Realizadas - Data: 2025-06-10
- Fiz login na plataforma do projeto.
- Baixei e organizei as planilhas de dados.
- Iniciei a etapa de conexão e importação de dados conforme a meta.
- Organizei as pastas no Google Drive e configurei o repositório no GitHub para versionamento.

---

## Atividades Realizadas - Data: 2025-06-11
- Analisei as tabelas do projeto e identifiquei valores nulos em duas delas.
- Na tabela `clientes`, detectei **24 células vazias** na coluna **salário anual**.
- Na tabela `compras`, identifiquei **7 células vazias** na coluna **ID dos clientes**.
- Registrei essas inconsistências para posterior tratamento dos dados.
- O tratamento dos valores nulos será feito conforme o impacto em futuras análises.

---

## Atividades Realizadas - Data: 2025-06-12
- Na tabela `clientes`, detectei **24 células vazias** na coluna **salário anual**. A estratégia adotada foi criar uma nova coluna chamada **salario_corrigido** e preencher com a mediana (valor: 51382).
- Na tabela `compras`, identifiquei **7 células vazias** na coluna **ID dos clientes**. A estratégia adotada foi remover as células pois a análise RFM, o id_cliente é essencial.
- iniciar o tratamento de dados duplicados: verificar se existem duplicatas nas tabelas.