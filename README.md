# 🛰️ Indoor Localization using Selective GANs

Implementação em Python (Jupyter Notebook) do artigo científico:  
**"Indoor Localization Using Data Augmentation via Selective Generative Adversarial Networks"**  
Este projeto tem como objetivo reproduzir os experimentos descritos no artigo, aplicando técnicas de Deep Learning e geração de dados sintéticos via GAN para melhorar a acurácia de localização indoor baseada em RSSI.

---

## 📌 Objetivos do Projeto

- 📡 Simular dados de RSSI utilizando modelo de propagação com ruído.
- 🧠 Gerar amostras sintéticas com **GANs** (Generator + Discriminator).
- 🏷️ Aplicar **pseudo-rotulação** supervisionada com DNN.
- 🧭 Selecionar os dados mais confiáveis com base em critérios estatísticos.
- 📍 Avaliar a acurácia de localização com e sem dados gerados.
- 🏢 Validar os resultados utilizando a base real **UJIndoorLoc**.

---

## 📁 Estrutura do Repositório

```bash
├── data/                 # Dados reais e simulados (UJIndoorLoc e gerados)
├── models/               # Modelos treinados (GAN, DNNs)
├── notebooks/            # Notebooks principais por etapa
├── outputs/              # Gráficos, tabelas e resultados
├── requirements.txt      # Dependências do projeto
├── README.md             # Este arquivo
└── notebook_final.ipynb  # Notebook consolidado com todo o pipeline
````

---

## 🚀 Como Executar

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/indoor-gan-localization.git
cd indoor-gan-localization
```

### 2. Crie um ambiente virtual e instale as dependências

```bash
python -m venv venv
source venv/bin/activate  # ou venv\Scripts\activate no Windows
pip install -r requirements.txt
```

### 3. Execute o notebook principal

```bash
jupyter notebook notebook_final.ipynb
```

---

## 📊 Principais Resultados

| Cenário                          | Erro Médio (m) | Melhoria (%)                                         |
| -------------------------------- | -------------- | ---------------------------------------------------- |
| Apenas dados reais               | x.xx           | —                                                    |
| Dados reais + GAN (sem seleção)  | x.xx           | +x.xx%                                               |
| Dados reais + GAN (selecionados) | x.xx           | **+21.96%** (simulados)<br>**+15.36%** (dados reais) |

---

## 📚 Referência do Artigo

> Han Zou, Xi Liu, Hao Jiang, Linlin Xie, and Costas Spanos.
> **Indoor Localization Using Data Augmentation via Selective Generative Adversarial Networks**
> In Proceedings of the 2021 ACM International Joint Conference on Pervasive and Ubiquitous Computing (UbiComp '21).
> DOI: [10.1145/3460418.3479275](https://doi.org/10.1145/3460418.3479275)

---

## 🧠 Sobre o Autor

Desenvolvido por **Oziel Ramos de Lima Junior**,
Cientista de Dados e Desenvolvedor Python com foco em IA, deep learning e análise de sequências pseudoaleatórias.

> 📬 Contato via GitHub: [@oziieljuniior](https://github.com/oziieljuniior)

---

## 📄 Licença

Este projeto é de caráter acadêmico e segue a licença [MIT](LICENSE), salvo menção explícita para uso de bases de dados externas (como UJIndoorLoc).


