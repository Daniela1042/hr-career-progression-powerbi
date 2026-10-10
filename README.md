# Dashboard de Progressões de Carreira em RH (Power BI)

Projeto desenvolvido na unidade curricular **Desenho e Desenvolvimento de Aplicações de Business Intelligence**, no Mestrado em Sistemas Integrados em Business Intelligence (ISCTE – Instituto Universitário de Lisboa), 2026.

O projeto cobre o ciclo completo de uma solução de BI: um **modelo dimensional em estrela** sobre dados de recursos humanos e um **dashboard interativo em Power BI** para analisar as progressões de carreira dos colaboradores.

## Objetivo

Perceber como evoluem as carreiras numa organização e responder a perguntas como:

- Quantas progressões houve ao longo do tempo e de que tipo foram?
- Que departamentos e áreas funcionais concentram mais progressões?
- Qual é o aumento médio e a taxa de variação salarial associados a cada progressão?
- Como se relacionam as progressões com a avaliação de desempenho, a antiguidade, a idade e o género?
- Que zonas geográficas concentram mais progressões?

## Modelo de dados

Modelo dimensional em estrela com **2 tabelas de factos** e **8 dimensões**.

| Tipo | Tabela | Descrição |
|------|--------|-----------|
| Facto | `Fact_Table_Progressao` | Uma linha por progressão individual |
| Facto | `Fact_Progressao_Agregada` | Progressões agregadas por departamento e período |
| Dimensão | `DateDimension` | Calendário (hierarquias de ano civil e fiscal) |
| Dimensão | `Dim_Colaborador` | Dados do colaborador (inclui género) |
| Dimensão | `Dim_Departamento` | Departamento e área funcional |
| Dimensão | `Dim_Tipo_Progressao` | Área e categoria da progressão |
| Dimensão | `Dim_Perfil_Avaliacao` | Perfil e intervalo de avaliação de desempenho |
| Dimensão | `Dim_Antiguidade` | Nível de experiência e tempo de antiguidade |
| Dimensão | `Dim_Idade` | Idade e faixa etária |
| Dimensão | `Dim_Local_trabalho` | País, distrito, concelho e freguesia |

<img width="1890" height="1325" alt="modelo_estrela" src="https://github.com/user-attachments/assets/64c82cdf-e073-4744-b64c-4c1e715b9e89" />


## Dashboard

O relatório tem **2 páginas** e **8 KPIs**, com medidas escritas em DAX.

### Progressões Individuais

- **KPIs:** total de progressões, aumento médio, taxa de variação salarial e distrito com mais progressões
- Evolução de progressões por ano
- Distribuição por tipo de progressão
- Distribuição por nível de avaliação
- Total de progressões por localização
- Progressões por nível de experiência e género
- Taxa de variação salarial por faixa etária e género
- Filtros por categoria de progressão, género, departamento, desempenho, ano, faixa etária e concelho



### Visão Agregada

- **KPIs:** total de progressões agregadas, departamento com mais progressões, média da taxa de variação e média do novo salário
- Total de progressões por área funcional
- Média de variação por área funcional
- Média do novo salário por ano fiscal
- Filtros por ano, categoria de progressão, departamento e área funcional


## Ferramentas

- Power BI Desktop (modelação, medidas DAX e visualização)
- Modelação dimensional (esquema em estrela)


└── docs/
    ├── dashboard.pdf
    ├── medidas_dax.md
    └── ficha_tecnica.pdf
```

