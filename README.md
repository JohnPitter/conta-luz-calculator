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
[Geracao Solar](#geracao-distribuida-solar) •
[Calculo](#calculo) •
[Privacidade](#privacidade)

</div>

---

## Overview

Ferramenta 100% client-side que extrai automaticamente os dados da sua fatura de energia e calcula o valor por pessoa. Nenhum dado e enviado para servidores — todo o processamento ocorre no seu navegador.

**O que voce obtem:**
- **Leituras e consumo** — Leitura anterior, atual e consumo do periodo em kWh
- **Geracao distribuida** — Detalha consumo medido, energia solar compensada e consumo faturado
- **Taxas** — TUSD e TE extraidas com precisao total (calculo) e exibidas com 4 casas decimais
- **Calculos** — Valor bruto, desconto percentual, valores adicionais e divisao por pessoa
- **Compartilhamento** — Envio do resumo pronto via WhatsApp
- **Privacidade** — Zero armazenamento, zero rastreamento, zero coleta

---

## Como Funciona

1. Faca upload do PDF da conta de luz (arrastar ou clicar)
2. Se o PDF estiver protegido, informe a senha quando solicitada
3. O sistema extrai automaticamente leituras e taxas:
   - PDFs com texto: leitura direta
   - PDFs em imagem (DANFE da Neoenergia): leitura via **OCR** automatico
4. Informe o percentual de desconto, o numero de pessoas e os valores adicionais
5. Veja o resultado por pessoa e, se quiser, envie o resumo via WhatsApp

> Faturas da Neoenergia costumam ser **PDFs de imagem** (sem texto selecionavel). Nesses casos o app renderiza cada pagina e aplica OCR (Tesseract.js) automaticamente — a primeira leitura baixa o dicionario de portugues (~10 MB) e fica em cache para as proximas.

---

## Dados Extraidos

| Campo | Descricao | Exemplo |
|-------|-----------|---------|
| Leitura Anterior | Registro do medidor no inicio do periodo | 12.348 |
| Leitura Atual | Registro do medidor no final do periodo | 12.926 |
| Consumo medido (total) | Diferenca das leituras (consumo bruto do relogio) | 578 kWh |
| Geracao solar (compensada) | Energia abatida pela geracao distribuida (linha CAT) | - 279,77 kWh |
| Consumo faturado | O que a distribuidora cobra (medido - geracao) | 298 kWh |
| Taxa TUSD | Tarifa de Uso do Sistema de Distribuicao | R$ 0,7190 |
| Taxa TE | Tarifa de Energia | R$ 0,3542 |

---

## Geracao Distribuida (Solar)

Contas com **geracao distribuida** (energia solar compartilhada) tem o consumo medido no relogio **maior** que o consumo faturado: a fatura abate a energia que a geracao solar compensou. Esse abatimento aparece na fatura como uma linha do tipo `CAT de - X kWh`.

```
Consumo medido (relogio)   = Leitura Atual - Leitura Anterior   (ex.: 12.926 - 12.348 = 578 kWh)
Geracao solar compensada   = ajuste CAT da fatura               (ex.: 279,77 kWh)
Consumo faturado           = Medido - Geracao                   (ex.: 578 - 279,77 = 298 kWh)
```

O calculo usa o **consumo medido (bruto)**, pois inclui a energia da geracao solar que tambem e paga. Quando o OCR nao consegue ler a linha fina do medidor, o consumo medido e reconstruido de forma confiavel como `faturado + geracao compensada` (matematicamente equivalente a diferenca das leituras).

Em contas **sem** geracao distribuida (sem linha CAT), o consumo medido e igual ao faturado e o detalhamento solar nao aparece.

---

## Calculo

```
Total Taxas        = TUSD + TE
Valor Bruto        = Consumo medido (kWh) x Total Taxas
Valor com Desconto = Valor Bruto - (Valor Bruto x Desconto%)
Valor Final        = Valor com Desconto + Valores Adicionais
Valor por Pessoa   = Valor Final / Total de Pessoas
```

O campo **Valores Adicionais** soma encargos/valores que ficam fora da energia descontada — por exemplo, no modelo de geracao compartilhada, a conta cheia paga a distribuidora.

### Exemplo

Fatura de junho (578 kWh medidos, desconto 30%, 2 pessoas, sem valores adicionais):

| Etapa | Formula | Resultado |
|-------|---------|-----------|
| Total Taxas | 0,71902181 + 0,35419760 | R$ 1,07321941 |
| Valor Bruto | 578 x 1,07321941 | R$ 620,32 |
| Desconto 30% | 620,32 x 0,30 | - R$ 186,10 |
| Valor com Desconto | 620,32 - 186,10 | R$ 434,22 |
| Valor por Pessoa (2) | 434,22 / 2 | **R$ 217,11** |

> Os calculos utilizam os valores exatos extraidos do PDF (precisao total), sem arredondamento intermediario. As taxas sao apenas **exibidas** com 4 casas decimais; o resultado final e arredondado para 2 casas.

---

## Tecnologias

| Tecnologia | Uso |
|------------|-----|
| HTML / CSS / JS | Interface e logica da aplicacao |
| [PDF.js](https://mozilla.github.io/pdf.js/) | Leitura e parsing do PDF no navegador |
| [Tesseract.js](https://tesseract.projectnaptha.com/) | OCR de PDFs em imagem (DANFE), 100% no navegador |
| GitHub Pages | Hospedagem estatica |
| Google Fonts | Tipografia (Outfit + DM Sans) |

---

## Privacidade

| Aspecto | Detalhe |
|---------|---------|
| Armazenamento | Nenhum dado e salvo, coletado ou enviado |
| Processamento | 100% no navegador do usuario (client-side) |
| PDF | Lido em memoria e descartado apos extracao |
| OCR | Executado localmente; apenas o dicionario do Tesseract e baixado/cacheado |
| Senha do PDF | Usada apenas em memoria para abrir o arquivo; nunca armazenada |
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

> O OCR depende de recursos carregados via CDN (Tesseract.js e PDF.js) e do download do dicionario de portugues, entao a leitura de PDFs em imagem precisa de conexao com a internet.

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
