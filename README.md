# Preços de imóveis e perfil construtivo — Brasil

Projeto acadêmico de coleta e análise de dados para a disciplina **Introdução à Ciência de Dados**.

**Autor:** Jedson Correa Leite  
**Data indicada no projeto:** 03/11/2026

## Objetivo

Comparar preços medianos anunciados por metro quadrado nas cinco Grandes Regiões do Brasil com o perfil dos domicílios segundo o material predominante nas paredes externas.

> **Limite importante:** a base de preços do Guru dos Imóveis não identifica o material construtivo de cada imóvel. A PNAD apresenta percentuais agregados por região. Portanto, o projeto compara indicadores regionais; não estima o preço individual de casas por material nem estabelece causalidade.

## Fontes

1. [Guru dos Imóveis — Dados Abertos](https://gurudosimoveis.com.br/dados): CSV por cidade, com séries mensais de preço mediano por m² por bairro e indicadores de anúncios. A página informa licença CC BY 4.0 e início da série em setembro de 2025.
2. [IBGE/SIDRA — PNAD Contínua, tabela 6822](https://sidra.ibge.gov.br/tabela/6822): percentual de domicílios por material predominante nas paredes, por Grande Região. A coleta é feita pela API SIDRA.

## Estrutura

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── projeto_coleta_imobiliario_brasil.ipynb
├── docs/
│   └── projeto_coleta_dados.md
├── dados/
│   └── (arquivos CSV e JSON gerados após a execução)
└── graficos/
    └── (gráficos PNG gerados após a execução)
```

## Como executar no Google Colab

1. Abra o notebook `notebooks/projeto_coleta_imobiliario_brasil.ipynb` no Google Colab.
2. Execute as células em ordem, começando pela Parte 1.
3. A coleta requer conexão com a internet.
4. Confira a cobertura das cinco regiões e o mês comum selecionado.
5. Ao final, os CSVs serão salvos na pasta `dados/`, os gráficos em `graficos/` e a documentação de resultados em `documentacao_resultados.md`.

Caso o ambiente não tenha alguma biblioteca, execute:

```python
!pip install -r requirements.txt
```

## Arquivos gerados

- `dados/imoveis_bairros.csv`
- `dados/precos_cidades.csv`
- `dados/perfil_construtivo_pnad.csv`
- `dados/integrado_regional.csv`
- `dados/metadados_coleta.json`
- `graficos/01_preco_mediano_regiao.png`
- `graficos/02_boxplot_precos_bairros.png`
- `graficos/03_material_paredes_regiao.png`
- `graficos/04_preco_vs_alvenaria.png`
- `documentacao_resultados.md`

Os números finais dependem dos dados efetivamente retornados no momento da execução. Nenhum valor foi pré-preenchido ou simulado.

## Publicação no GitHub

Crie um repositório chamado `analise-imobiliaria-material-brasil` e envie o conteúdo desta pasta mantendo a estrutura acima. Depois, para abrir no Colab, use a opção **Arquivo > Abrir notebook > GitHub** e informe o endereço do repositório.

## Limitações

- Preços anunciados não equivalem a preços efetivamente transacionados.
- A cobertura de cidades não é uniforme entre regiões.
- O Norte possui menos cidades listadas na fonte consultada.
- O material construtivo não está associado a cada anúncio.
- A síntese regional é uma mediana das cidades selecionadas, não uma média ponderada da população ou do estoque imobiliário.
- Preços mensais e estimativas anuais da PNAD têm frequências distintas.

## Referências

- GURU DOS IMÓVEIS. Dados abertos do mercado imobiliário brasileiro. https://gurudosimoveis.com.br/dados.
- IBGE. SIDRA, tabela 6822 — Domicílios e Moradores, por material predominante nas paredes. https://sidra.ibge.gov.br/tabela/6822.
