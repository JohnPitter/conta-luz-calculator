# Calculadora de Conta de Luz

<div align="center">

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=for-the-badge&logo=githubpages&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Calculadora gratuita para faturas da Neoenergia Pernambuco**

*Envie o PDF da sua conta de luz e obtenha o valor por pessoa com desconto*

[Acessar Calculadora](https://johnpitter.github.io/conta-luz-calculator/) •
[Como Funciona](#como-funciona) •
[Calculo](#calculo) •
[Privacidade](#privacidade)

</div>

---

## Overview

Ferramenta 100% client-side que extrai automaticamente os dados da sua fatura de energia e calcula o valor por pessoa. Nenhum dado e enviado para servidores — todo o processamento ocorre no seu navegador.

**O que voce obtem:**
- **Leituras** — Leitura anterior, atual e consumo total em kWh
- **Taxas** — TUSD e TE extraidas com precisao total (8 casas decimais)
- **Calculos** — Valor bruto, desconto percentual e divisao por pessoa
- **Privacidade** — Zero armazenamento, zero rastreamento, zero coleta

---

## Como Funciona

1. Faca upload do PDF da conta de luz (arrastar ou clicar)
2. O sistema extrai automaticamente leituras e taxas do PDF
3. Informe o percentual de desconto e o numero de pessoas na casa
4. Veja o resultado final por pessoa

---

## Dados Extraidos

| Campo | Descricao | Exemplo |
|-------|-----------|---------|
| Leitura Anterior | Registro do medidor no inicio do periodo | 9.251 |
| Leitura Atual | Registro do medidor no final do periodo | 10.049 |
| Consumo (kWh) | Diferenca entre leituras | 798 |
| Taxa TUSD | Tarifa de Uso do Sistema de Distribuicao | R$ 0,52040968 |
| Taxa TE | Tarifa de Energia | R$ 0,30022404 |

---

## Calculo

```
Total Taxas       = TUSD + TE
Valor Bruto       = Consumo (kWh) x Total Taxas
Valor com Desconto = Valor Bruto - (Valor Bruto x Desconto%)
Valor por Pessoa  = Valor com Desconto / Total de Pessoas
```

### Exemplo

| Etapa | Formula | Resultado |
|-------|---------|-----------|
| Total Taxas | 0,52040968 + 0,30022404 | R$ 0,82063372 |
| Valor Bruto | 798 x 0,82063372 | R$ 654,87 |
| Desconto 30% | 654,87 x 0,30 | - R$ 196,46 |
| Valor com Desconto | 654,87 - 196,46 | R$ 458,41 |
| Valor por Pessoa (2) | 458,41 / 2 | **R$ 229,20** |

> Os calculos utilizam os valores exatos extraidos do PDF (8 casas decimais), sem arredondamento intermediario. Apenas o resultado final e arredondado para 2 casas.

---

## Tecnologias

| Tecnologia | Uso |
|------------|-----|
| HTML / CSS / JS | Interface e logica da aplicacao |
| [PDF.js](https://mozilla.github.io/pdf.js/) | Leitura e parsing do PDF no navegador |
| GitHub Pages | Hospedagem estatica |
| Google Fonts | Tipografia (Outfit + DM Sans) |

---

## Privacidade

| Aspecto | Detalhe |
|---------|---------|
| Armazenamento | Nenhum dado e salvo, coletado ou enviado |
| Processamento | 100% no navegador do usuario (client-side) |
| PDF | Lido em memoria e descartado apos extracao |
| Cookies | Nenhum cookie utilizado |
| Analytics | Nenhum rastreador de usuario |

---

## Compatibilidade

| Distribuidora | Status |
|---------------|--------|
| Neoenergia Pernambuco (CELPE) | ✅ Testado |
| Outras distribuidoras | ❌ Nao suportado |

### Navegadores

| Navegador | Status |
|-----------|--------|
| Chrome 90+ | ✅ |
| Firefox 90+ | ✅ |
| Safari 15+ | ✅ |
| Edge 90+ | ✅ |
| Mobile (iOS/Android) | ✅ |

---

## Executando Localmente

Nao requer instalacao. Basta abrir o arquivo `index.html` no navegador:

```bash
git clone https://github.com/JohnPitter/conta-luz-calculator.git
cd conta-luz-calculator
# Abra index.html no navegador ou use um servidor local:
python -m http.server 8080
```

Acesse `http://localhost:8080`

---

## Estrutura do Projeto

```
conta-luz-calculator/
├── index.html        # Aplicacao completa (HTML + CSS + JS)
├── favicon.svg       # Icone do site (SVG)
├── favicon.ico       # Icone do site (fallback)
├── robots.txt        # Configuracao para crawlers
├── sitemap.xml       # Mapa do site para buscadores
└── README.md         # Documentacao
```

---

## Licenca

Este projeto e open source e gratuito para uso pessoal.

---

## Suporte

- **Issues:** [GitHub Issues](https://github.com/JohnPitter/conta-luz-calculator/issues)
