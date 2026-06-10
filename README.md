# 🚀 Stellar Classification Project - Global Solution 2026

**Disciplina:** Generative AI For Engineering (GAIE)

**Tema:** Aplicação de Machine Learning em Dados Astronômicos para a Indústria Espacial

---

## 🧑‍💻 Integrantes
| Nome | RM |
|---|---|
| Lucas Moreno | RM 97158 |
| Lorenzo Gomes | RM 551117 |
| Leonardo Schunck Rainha | RM 99902 |
| Kayky Oliveira Schunck | RM 99756 |


---

## 🌌 1. Contexto do Problema: A Nova Corrida Espacial
O espaço é um domínio cada vez mais movido por dados e software. A capacidade de analisar grandes volumes de dados de sensoriamento remoto e telescópios é crucial para a exploração espacial, desde o mapeamento de detritos até a identificação de novos corpos celestes.

**Problema:** Classificar objetos celestes (estrelas, galáxias e quasares - QSO) a partir de dados de magnitude espectroscópica (SDSS).
**Relevância para a Indústria Espacial:** A correta classificação de objetos é fundamental para:
1.  **Mapeamento de Alvos:** Direcionar telescópios e missões espaciais para os alvos de maior interesse (ex: galáxias ativas).
2.  **Monitoramento:** Distinguir fontes de luz naturais (estrelas) de fontes de interesse científico (galáxias/QSO).
3.  **Análise de Dados:** Fornecer um sistema automatizado e robusto para processar o fluxo constante de dados orbitais.

---

## 🎯 2. Objetivo do Projeto
Desenvolver um *pipeline* completo de Machine Learning para classificar objetos celestes em três categorias (`STAR`, `GALAXY`, `QSO`) utilizando dados de magnitude espectroscópica (SDSS). O projeto visa demonstrar a capacidade de construir uma solução de IA robusta, interpretável e *deployável* para o setor espacial.

---

## 🛠️ 3. Metodologia e Pipeline de ML

O projeto segue um pipeline de Machine Learning completo, dividido em etapas de exploração, modelagem e interpretação:

### 3.1. Exploração e Engenharia de Dados
*   **Dataset:** Utilizado o dataset SDSS DR19, contendo magnitudes em diferentes bandas espectrais (`u`, `g`, `r`, `i`, `zband`) e dados de movimento próprio.
*   **Engenharia de Features:** Foram criadas *features* derivadas, como a correção de extinção de poeira (`r_corr`) e índices de cores (`u_g`, `g_r`, `r_i`, `i_z`), que aumentam o poder discriminatório do modelo.
*   **Análise Exploratória:** Foi realizada uma análise de *pairplot* e clusterização K-Means para verificar a separabilidade das classes apenas com magnitudes UV e IR.

### 3.2. Modelagem e Comparação de Modelos
*   **Técnicas Testadas:**
    *   **K-Means Clustering:** Usado para verificar a separabilidade intrínseca dos dados.
    *   **PyCaret (AutoML):** Comparou diversas arquiteturas de ML, identificando o **XGBoost** como o modelo de melhor performance.
*   **Modelo Final:** **XGBoost Classifier** foi selecionado por sua robustez, eficiência e alta performance em dados tabulares.
*   **Pré-processamento:** Foi aplicado o escalonamento de dados e a remoção de *features* com baixa contribuição (identificadas via análise de importância de features).

### 3.3. Validação e Interpretabilidade
*   **Métricas:** O modelo foi avaliado usando Acurácia, *Recall*, *Precision* e o **Score F1** (via `classification_report`), garantindo uma visão completa do desempenho em cada classe.
*   **Matriz de Confusão:** Apresentada em modo normalizado, permitindo entender a taxa de erro por classe.
*   **SHAP (SHapley Additive exPlanations):** Utilizado para garantir a **interpretabilidade** do modelo. O SHAP revela quais *features* (ex: `u_g`, `zband`) têm maior influência na decisão de classificação, permitindo que o cientista explique *por que* o modelo classificou um objeto de determinada maneira.

### 3.4. Deploy da Solução
*   **Interface:** Foi construído um protótipo funcional utilizando a biblioteca **Gradio**.
*   **Funcionalidade:** O usuário pode inserir manualmente os 16 atributos físicos e derivados de um objeto celeste e receber a classificação predita (`STAR`, `GALAXY` ou `QSO`) em tempo real.

---

## 📈 4. Resultados e Análise

**Métricas de Teste:**
*   **Acurácia:** 95.51%
*   **Recall (GALAXY):** 98% (Indica a capacidade de encontrar todas as galáxias)
*   **F1-Score (QSO):** 89%

**Análise SHAP:**
O SHAP confirmou que a combinação de **índices de cor** (como `u_g` e `g_r`) e a **Petrosian radius** (`petroR50_r`) são fatores fortemente determinantes para a distinção entre as classes, validando a hipótese física do projeto.

---

## 🚀 5. Conclusão e Impacto na Indústria Espacial
Este projeto não é apenas um exercício de ML; é um protótipo de um sistema de inteligência artificial que pode ser integrado a plataformas de análise de dados orbitais.

**Impacto:** A capacidade de classificar objetos em tempo real, com alta precisão e interpretabilidade, é vital para:
1.  **Missões de Observação:** Filtrar dados brutos para focar apenas em alvos de interesse científico.
2.  **Detecção de Anomalias:** Identificar rapidamente objetos que não se encaixam nos padrões conhecidos, sinalizando possíveis eventos ou detritos.

---

## ⚙️ 6. Como Executar o Projeto
1. **Clonar o Repositório:**
    ```bash
    git clone https://github.com/LM2124/Fiap-2026-GlobalSolution1-GenAI.git
    cd Fiap-2026-GlobalSolution1-GenAI
    ```
2. **Ambiente Virtual e Dependências:**
    Instale as dependências usando [`uv`](https://docs.astral.sh/uv/getting-started/installation/) para garantir um ambiente rápido e isolado.
    ```bash
    uv sync
    ```
3. **Execução (Jupyter Notebook):**
    Execute o notebook `main.ipynb` no ambiente Jupyter usando o comando:
    ```bash
    uv run jupyter notebook main.ipynb
    ```
    > *Alternativamente, você pode executar o notebook diretamente em um ambiente de IDE como o VS Code.*
4. **Resultado:**
    O último bloco de código (Gradio) iniciará um servidor local, permitindo a interação com o classificador.
