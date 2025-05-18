# ✅ Visão Geral da Fase 2

A Fase 2 consiste em **treinar um GAN simples** (com uma camada escondida em cada rede), para que o **Generator aprenda a criar vetores RSSI realistas**, indistinguíveis dos reais pelo Discriminator.

---

## 🧠 Estrutura do GAN

### 🎯 Objetivo:

* **Entrada do Generator**: vetor de ruído $z \sim \mathcal{U}(-1, 1)^{10}$
* **Saída do Generator**: vetor de RSSI com 10 valores (simulando os 10 APs)
* **Discriminator**: tenta diferenciar vetores reais de vetores gerados
* **Treinamento adversarial**: Generator tenta enganar o Discriminator

---

## 🗂️ Preciso de banco de dados?

### ❌ **Você NÃO precisa carregar um banco externo agora.**

Você **já possui os dados simulados reais**, que são os **1000 vetores RSSI reais**, salvos em `df_simulated.csv`. Eles devem ser carregados (ou mantidos em memória) no início da Etapa 2:

```python
# Se quiser recarregar do CSV (opcional)
df_simulated = pd.read_csv("data/df_simulated.csv")
X_real = df_simulated.iloc[:, :10].values.astype(np.float32)
```

---

## 🔧 Etapas da Implementação – Explicadas

### ✅ 1. **Pré-processamento**

* Extraia os 10 primeiros campos de cada vetor (`WAP001` a `WAP010`)
* Normalize se necessário (não essencial, pois valores já estão em faixa comum de dBm)

### ✅ 2. **Definir as arquiteturas**

* `Generator`: input=(10,), Dense(10 ReLU), Dense(10 linear)
* `Discriminator`: input=(10,), Dense(10 ReLU), Dense(1 sigmoid)

### ✅ 3. **Compilar os modelos**

* `Discriminator`: binária, `loss='binary_crossentropy'`, `Adam(0.01)`
* `GAN`: conecta G → D, e compila com mesmo loss/otimizador

### ✅ 4. **Treinar por 200 épocas**

* Em cada época:

  * Gerar amostras fake: `G(z)`
  * Misturar com amostras reais: `X_real`
  * Treinar o Discriminator separadamente com:

    * 50% reais (label=1), 50% fakes (label=0)
  * Depois congelar o Discriminator e treinar o Generator via GAN com `label=1` (engane o D)

### ✅ 5. **Salvar perdas (losses)**

* Guardar os valores `loss_d` e `loss_g` por época para plotar depois

### ✅ 6. **Gerar vetores RSSI sintéticos**

* Após treino, usar `generator.predict(z)` com `z.shape = (40000, 10)`
* Salvar `df_generated.csv` para as próximas fases

---

## ⚠️ Coisas para ficar atento

### 🔹 Overfitting do Discriminator:

* Se o Discriminator ficar muito bom, o Generator para de melhorar
* Use aprendizado balanceado (re-treine o D e o G alternadamente)

### 🔹 Geração fora da faixa esperada:

* RSSI deve ficar entre \~\[-110, -40]
* Pode ser necessário aplicar `np.clip(v, -110, -40)` na saída do Generator

### 🔹 Perda instável (normal em GANs):

* Flutuações de `loss_d` e `loss_g` são esperadas, mas devem convergir levemente

---

## ✅ Resumo da Estrutura

```text
| Parte                    | Tarefa                                     |
|--------------------------|--------------------------------------------|
| Dados reais              | 1000 vetores do df_simulated (WAP001–010) |
| Generator                | Densa (10 ReLU) → Densa (10 linear)       |
| Discriminator            | Densa (10 ReLU) → Densa (1 sigmoid)       |
| Perda                    | BCE (binary cross-entropy)                |
| Otimizador               | Adam (lr=0.01)                             |
| Treinamento              | 200 épocas, alternando D e G              |
| Saída final              | 40000 vetores sintéticos (para fase 3)    |
```

---

