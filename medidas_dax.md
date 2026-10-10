# Medidas DAX

Medidas usadas nos KPIs e visuais do dashboard.

## Página "Progressões Individuais" (`Fact_Table_Progressao`)

### Total Progressoes
Número de progressões registadas.
```dax
Total Progressoes = COUNTROWS('dw Fact_Table_Progressao')
```

### Aumento Medio
Aumento salarial médio por progressão.
```dax
Aumento Medio = AVERAGE('dw Fact_Table_Progressao'[aumento_salarial])
```

### Taxa Variacao Salarial
Soma dos aumentos salariais dividida pela soma dos salários anteriores. O `DIVIDE` devolve 0 quando o denominador é zero.
```dax
Taxa Variacao Salarial =
DIVIDE(
    SUM('dw Fact_Table_Progressao'[aumento_salarial]),
    SUM('dw Fact_Table_Progressao'[salario_antigo]),
    0
)
```

### Custo Salarial Total
Soma dos novos salários.
```dax
Custo Salarial Total = SUM('dw Fact_Table_Progressao'[salario_novo])
```

### Top Distrito
Distrito com mais progressões no contexto de filtros atual. Cria uma tabela temporária com o total por distrito e devolve o primeiro (`TOPN 1`).
```dax
Top Distrito =
VAR Tabela =
    ADDCOLUMNS(
        VALUES('dw Dim_Local_trabalho'[distrito]),
        "Total", CALCULATE([Total Progressoes])
    )
VAR Top1 =
    TOPN(1, Tabela, [Total], DESC)
RETURN
    MAXX(Top1, 'dw Dim_Local_trabalho'[distrito])
```

## Página "Visão Agregada" (`Fact_Progressao_Agregada`)

### Total Progressoes Agr
Total de progressões na tabela agregada.
```dax
Total Progressoes Agr = SUM('dw Fact_Progressao_Agregada'[total_progressoes])
```

### Top Departamento
Departamento com mais progressões agregadas.
```dax
Top Departamento =
MAXX(
    TOPN(1, VALUES('dw Dim_Departamento'[designacao_departamento]), [Total Progressoes Agr], DESC),
    'dw Dim_Departamento'[designacao_departamento]
)
```

### Total Aumento Agr
Soma dos aumentos salariais na tabela agregada.
```dax
Total Aumento Agr = SUM('dw Fact_Progressao_Agregada'[total_aumento_salarial])
```

### Media Taxa Variacao Agr
Média do aumento salarial médio por linha agregada. A medida `media_variacao_pct` tem a mesma fórmula e alimenta o gráfico "Média de Variação por Área Funcional".
```dax
Media Taxa Variacao Agr = AVERAGE('dw Fact_Progressao_Agregada'[media_aumento_salarial])
```

### Media Salario Novo Agr
Média do novo salário, calculada sobre a tabela de factos detalhada.
```dax
Media Salario Novo Agr = AVERAGE('dw Fact_Table_Progressao'[salario_novo])
```

## Texto de atualização

### Última Atualização
Texto com a data e hora atuais, usado no rodapé das duas páginas.
```dax
Última Atualização = "Última atualização: " & FORMAT(NOW(), "dd/MM/yyyy HH:mm")
```
