# Proposta Técnica – Implementação do Artigo "Indoor Localization Using Data Augmentation via Selective GANs"

## Objetivo Geral

Implementar, em Python (formato Jupyter Notebook), a metodologia apresentada no artigo, com foco em:

* Geração de dados sintéticos de RSSI via **GANs**.
* Rotulagem automática com **DNN supervisionado**.
* Seleção inteligente dos dados gerados com base em **realismo estatístico** e **cobertura espacial**.
* Avaliação de desempenho em:

  * Cenário simulado (dados sintéticos baseados em modelo de propagação).
  * Cenário real (base **UJIndoorLoc** da UCI).

---

## Estrutura do Projeto (Resumo por Seções)

### 1. Introdução

* Descrição do problema de localização indoor.
* Justificativa da abordagem com GANs + pseudo-label.

### 2. Preparação de Dados

* Geração de RSSI sintético com fórmula de path loss e ruído (shadowing).
* Pré-processamento da base UJIndoorLoc (Building 1, Floor 2).

### 3. Arquitetura GAN

* Generator e Discriminator com camadas simples (10 neurônios).
* Treinamento adversarial com função de perda binária.

### 4. Pseudo-rotulação + Seleção

* Uso de DNN supervisionado para rotular os dados falsos.
* Seleção dos dados com base em:

  * Critério 1: Zonas espaciais (1m²).
  * Critério 2: Score do discriminador para "realismo".

### 5. Treinamento Final e Avaliação

* Modelo final treinado com dados reais + gerados selecionados.
* Avaliação por erro médio de localização (em metros).
* Reproduzir Figuras (4 a 6) e Tabelas (2 e 3) do artigo.

---

## Resultados Esperados

* **Simulação**: redução de até **21.96%** no erro com dados sintéticos.
* **Base real (UJIndoorLoc)**: melhora de até **15.36%** na acurácia.
* Visualizações como CDFs e mapas de erro.

---

## Aplicabilidade

* O projeto simula um caso real de localização indoor usando apenas **pequenos conjuntos rotulados**.
* Serve de base para soluções em **IoT, robótica, logística e rastreamento indoor**.

