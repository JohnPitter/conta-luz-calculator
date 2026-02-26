# Calculadora de Conta de Luz

Calculadora gratuita para faturas da **Neoenergia Pernambuco** (antiga CELPE). Envie o PDF da sua conta de luz e obtenha automaticamente o valor por pessoa com desconto.

**[Acessar a calculadora](https://johnpitter.github.io/conta-luz-calculator/)**

## Como funciona

1. Faca upload do PDF da conta de luz
2. O sistema extrai automaticamente as leituras e taxas
3. Informe o percentual de desconto e o numero de pessoas
4. Veja o resultado final por pessoa

## Dados extraidos do PDF

| Campo | Exemplo |
|-------|---------|
| Leitura Anterior | 9.251 |
| Leitura Atual | 10.049 |
| Consumo (kWh) | 798 |
| Taxa TUSD | R$ 0,52040968 |
| Taxa TE | R$ 0,30022404 |

## Calculo

```
Total Taxas = TUSD + TE
Valor Bruto = Consumo (kWh) x Total Taxas
Valor com Desconto = Valor Bruto - Desconto (%)
Valor por Pessoa = Valor com Desconto / Total de Pessoas
```

Os calculos utilizam os valores exatos extraidos do PDF (8 casas decimais), sem arredondamento intermediario.

## Privacidade

- Nenhum dado e armazenado, coletado ou enviado para servidores
- Todo o processamento ocorre no navegador do usuario (client-side)
- O PDF e lido em memoria e descartado apos a extracao

## Tecnologias

- HTML / CSS / JavaScript (vanilla)
- [PDF.js](https://mozilla.github.io/pdf.js/) para leitura do PDF no navegador
- GitHub Pages para hospedagem

## Compatibilidade

Desenvolvido e testado com faturas da **Neoenergia Pernambuco**. Outros formatos de conta de luz podem nao ser reconhecidos.

## Licenca

Este projeto e open source e gratuito para uso pessoal.
