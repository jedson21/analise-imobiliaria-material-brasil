# PROJETO DE COLETA DE DADOS
## Preços de imóveis e perfil construtivo por material nas cinco regiões do Brasil

**Autor:** Jedson Correa Leite  
**Data:** 03/11/2026  
**Disciplina:** Introdução à Ciência de Dados

---

## 1. OBJETIVO

Coletar e integrar dados públicos de preços anunciados de imóveis e de características construtivas dos domicílios brasileiros, comparando as cinco Grandes Regiões do Brasil. O foco construtivo será o material predominante nas paredes externas: alvenaria/taipa com revestimento, alvenaria/taipa sem revestimento, madeira apropriada para construção e outros materiais.

**Pergunta orientadora:** como os preços medianos anunciados por metro quadrado nas cidades selecionadas se distribuem entre as cinco regiões e como esse cenário se relaciona, de forma exploratória, com a composição regional dos domicílios segundo o material predominante das paredes?

**Delimitação metodológica importante:** a base de preços disponibiliza valores agregados por bairro/cidade, mas não informa o material construtivo de cada imóvel anunciado. A PNAD, por sua vez, informa percentuais de domicílios por material em escala regional, e não o preço de cada imóvel. Portanto, este projeto compara indicadores regionais em conjunto; **não estima o preço de imóveis individualmente condicionado ao material de construção**, nem demonstra causalidade.

## 2. FONTES DE DADOS

| Fonte | URL | Método | Dados coletados |
|---|---|---|---|
| Guru dos Imóveis – Dados Abertos | https://gurudosimoveis.com.br/dados | Download de CSV por cidade via HTTP | Mês, bairro, transação, mediana do preço por m², percentis, anúncios ativos e dias no mercado |
| IBGE – PNAD Contínua, SIDRA tabela 6822 | https://sidra.ibge.gov.br/tabela/6822 | API REST pública (JSON) | Percentual de domicílios por material predominante nas paredes, por Grande Região |

## 3. METODOLOGIA

### 3.1 Coleta
O notebook consulta a página de dados abertos do Guru dos Imóveis, identifica os links CSV das cidades selecionadas nas cinco regiões e baixa os arquivos. Depois consulta a API SIDRA do IBGE para obter a distribuição percentual dos domicílios por material predominante nas paredes, usando o ano de 2025 (último período disponível na tabela consultada na preparação do projeto).

### 3.2 Limpeza
São padronizados os nomes das colunas, os textos das categorias, as cidades e as regiões. As variáveis numéricas são convertidas para tipo numérico; registros sem preço mediano válido são removidos; são mantidas apenas observações de venda e o último mês comum entre as cidades selecionadas. Valores não disponíveis da API do IBGE são tratados como ausentes, sem substituição artificial.

### 3.3 Processamento
Os preços por bairro são resumidos primeiro por cidade (mediana das medianas de bairro). Para cada região, calcula-se a mediana dos indicadores das cidades selecionadas. Cada cidade tem o mesmo peso nessa síntese regional; não se trata de média ponderada pela população ou pelo total de imóveis da região. Os percentuais da PNAD são organizados em formato tabular e integrados por Grande Região. A comparação final é descritiva e exploratória.

## 4. DATASET FINAL

Os totais de registros, colunas, período e tamanho serão preenchidos automaticamente ao executar o notebook, pois dependem dos CSVs efetivamente disponibilizados na data da coleta.

Arquivos previstos:
- `imoveis_bairros.csv`: observações de preço por bairro, cidade e mês.
- `precos_cidades.csv`: resumo de preço por cidade.
- `perfil_construtivo_pnad.csv`: percentuais por região e material.
- `integrado_regional.csv`: preço regional e perfil de materiais em uma linha por região.
- `documentacao_resultados.md`: documentação preenchida com os resultados da execução.

## 5. ANÁLISE EXPLORATÓRIA

### 5.1 Estatísticas descritivas
Serão apresentados quantidade de bairros e cidades observadas, mediana, média, desvio-padrão, mínimo e máximo dos preços medianos por m², além dos percentuais regionais por material das paredes.

### 5.2 Visualizações
1. Gráfico de barras do preço mediano por m² nas regiões (mediana das cidades selecionadas).
2. Boxplot das medianas de preço por bairro, agrupadas por região.
3. Gráfico de barras agrupadas com o percentual de domicílios por material das paredes.
4. Gráfico exploratório comparando o preço regional e o percentual de domicílios com alvenaria/taipa com revestimento.

## 6. INSIGHTS

Os insights serão redigidos somente após a execução e a conferência dos dados reais. O notebook imprimirá perguntas orientadoras e evitará conclusões causais.

## 7. LIMITAÇÕES

- Os valores do Guru dos Imóveis são medianas de anúncios, não preços efetivamente transacionados.
- A cobertura de cidades é desigual entre regiões; a Região Norte tem menor quantidade de cidades disponíveis na página de dados consultada.
- A base de preços não informa o material de construção de cada imóvel.
- A PNAD apresenta estimativas amostrais regionais; não é uma base de avaliação individual de imóveis.
- As duas fontes têm periodicidades e unidades de observação distintas.
- A mediana regional é calculada a partir das cidades selecionadas, sem ponderação populacional, e não representa necessariamente toda a região.

## 8. PRÓXIMOS PASSOS

- Ampliar a lista de cidades à medida que novos CSVs forem disponibilizados.
- Buscar, em etapa futura, uma base de anúncios individualizados com atributo explícito e verificável de material construtivo, respeitando os termos de uso da fonte.
- Acrescentar variáveis de localização, tipologia e área quando houver dados comparáveis.

## 9. CÓDIGO

Notebook: `notebooks/projeto_coleta_imobiliario_brasil.ipynb`  
Ambiente de execução: Google Colab.  
Repositório GitHub sugerido: `analise-imobiliaria-material-brasil` (substituir pelo endereço criado pelo autor).

## 10. REFERÊNCIAS

- GURU DOS IMÓVEIS. **Dados abertos do mercado imobiliário brasileiro**. Disponível em: https://gurudosimoveis.com.br/dados. Acesso em: 09 nov. 2026.
- IBGE. **Pesquisa Nacional por Amostra de Domicílios Contínua – PNAD Contínua: tabela 6822, Domicílios e Moradores, por material predominante nas paredes**. SIDRA. Disponível em: https://sidra.ibge.gov.br/tabela/6822. Acesso em: 09 nov. 2026.
- IBGE. **Pesquisa Nacional por Amostra de Domicílios Contínua: características gerais dos domicílios e dos moradores**. Disponível em: https://www.ibge.gov.br/estatisticas/sociais/trabalho/17270-pnad-continua.html. Acesso em: 09 nov. 2026.
