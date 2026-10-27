# Detecção simples de anomalias com PySpark

Notebook mínimo que calcula a variação percentual mês a mês de uma série sintética de vendas e interrompe o pipeline quando a variação absoluta supera um limite.

**Estado:** exemplo didático isolado. Não há pacote, dados externos, testes ou execução reproduzida fora de um ambiente Spark.

## Lógica

O notebook:

1. cria quatro linhas sintéticas;
2. usa `lag` em uma janela ordenada por mês;
3. calcula a variação percentual;
4. filtra valores acima de `THRESHOLD = 150`;
5. lança uma exceção se houver anomalia;
6. grava `gold.vendas_mensais` somente no caminho sem anomalias.

## Executar

Importe `01_analyzing_anomalies.ipynb` em um ambiente com PySpark e uma sessão `spark` disponível, como Databricks.

## Limitações

- a amostra possui apenas quatro meses;
- o limite é arbitrário e não foi calibrado;
- não há tratamento para divisão por zero, sazonalidade ou dados ausentes;
- a falha detectada é intencional: março cresce 200% sobre fevereiro;
- o notebook demonstra uma regra, não um sistema de observabilidade.

Próximo passo: extrair a regra para uma função testável, parametrizar o limite e registrar evidências de casos válidos e inválidos.
