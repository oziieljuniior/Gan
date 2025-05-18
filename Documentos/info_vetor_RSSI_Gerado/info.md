# Comparação do Modelo de Propagação de RSSI

## **Modelo do Artigo (Equação 5 e 6)**

O artigo define o RSSI como:

$$
p_{ij} = pt - PL_{ij} + \mathcal{N}(0, \sigma)
$$

Onde o path loss $PL_{ij}$ é:

$$
PL_{ij} = PL_0 + 20 \log_{10}(f) + 10 \mu \log_{10}\left(\frac{d_{ij}}{d_0}\right)
$$

**Parâmetros usados no artigo (Tabela 1):**

* $pt = 20$ dBm
* $PL_0 = 40$ dB
* $f = 2.4 \text{GHz}$
* $\mu = 3.5$ (expoente típico indoor)
* $\sigma = 2$ (shadowing)
* $d_0 = 1$ m
* Número de APs: 10
* Área: 20 × 20 m² (400 zonas de 1 m²)

---

## **Seu Código (vetor\_RSSI\_simulado.pdf)**

Seu código Python realiza exatamente isso:

```python
path_loss = pl0 + 20 * np.log10(frequency) + 10 * mu * np.log10(d / d0)
noise = np.random.normal(0, sigma)
rssi = pt - path_loss + noise
```

Com:

* $pt = 20$, $pl0 = 40$, $\mu = 3.5$, $\sigma = 2$
* Frequência: $2.4 \times 10^9$ Hz
* Ruído Gaussiano
* Truncamento inferior: `rssi = max(rssi, -110)`

**Conclusão**: **Seu modelo está 100% fiel ao modelo descrito no artigo**, inclusive com os mesmos valores de parâmetros e estrutura.

---

# Gráficos e Visualizações

O artigo apresenta visualmente (Figuras 3 a 6):

* **Distribuição dos pontos de treino e teste**
* **Cobertura do ambiente**
* **Exemplos de cobertura parcial versus total ao variar a quantidade de amostras geradas**

Seu notebook também já gera:

* Posição dos **APs aleatórios**
* Posições **uniformemente distribuídas para treino**
* Posições **aleatórias para teste (2 por zona)**

🔍 O artigo mostra que:

* 100 posições (1 por zona) com 10 medições cada → 1000 vetores reais
* 800 posições de teste → 8000 vetores
* RSSIs simulados com mesma fórmula, incluindo ruído

---

# Próximos passos sugeridos:

1. **Salvar os gráficos comparáveis às Figuras do artigo**:

   * Figura 3 (posições reais)
   * Figura 4 (cobertura gerada com poucas amostras)
   * Figura 5a e 5b (comparação de cobertura com e sem seleção)
   * Figura 6 (CDF dos erros)

2. **Anotar no notebook esses comparativos** com legendas semelhantes, por exemplo:

   ```markdown
   **Figura 3 - Distribuição dos Pontos de Treino/Teste em Ambiente Simulado**
   ```

   Isso te ajuda na Etapa 5 (documentação e replicação visual).

3. **Comparar estatisticamente**:

   * Média e desvio dos RSSIs simulados
   * Distribuição dos vetores simulados vs. reais (após gerar reais com UJIndoorLoc)
