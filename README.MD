# Global Solution 2026-2 — Citizen Intelligence & Predictive Analytics
## Análise Preditiva de Mobilidade e Risco Viário na Rodovia BR-116 (Régis Bittencourt)

**Instituição:** FIAP — Faculdade de Informática e Administração Paulista  
**Curso:** Bacharelado em Ciência da Computação (Turma 2CCPB)  

**Integrantes da Equipe:**
* Matheus Guedes Grigorio — RM: 568086
* Vinicius Fernandes Silva Souza — RM: 567977

---

## Sobre o Projeto

Este repositório contém o pipeline completo de Ciência de Dados desenvolvido para investigar a dinâmica de tráfego, o impacto climático e a severidade de sinistros no corredor da **Rodovia BR-116 (trecho Régis Bittencourt — SP/PR)**, utilizando bases públicas oficiais da **Polícia Rodoviária Federal (PRF)** e da **Agência Nacional de Transportes Terrestres (ANTT)** referentes ao ano-base de 2025.

O objetivo central é responder como condições meteorológicas, horários do dia e características geométricas da via influenciam o fluxo de veículos, o tempo de deslocamento e a probabilidade de acidentes de alto impacto operacional, utilizando modelos de Machine Learning para antecipar cenários críticos e apoiar a tomada de decisão preventiva.

---

## Instalação das Dependências

Certifique-se de ter o **Python 3.10+** instalado em seu ambiente. Para instalar todas as bibliotecas necessárias para a execução do notebook, execute o comando abaixo no terminal:

```bash
pip install pandas numpy scikit-learn tensorflow plotly folium seaborn matplotlib joblib jupyter
```

---

## Como Executar o Projeto

### 1. Preparação do Ambiente Local
1. Clone este repositório para a sua máquina local:
   ```bash
   git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
   cd seu-repositorio
   ```
2. Instale as dependências listadas na seção anterior.
3. Certifique-se de que os arquivos de dados brutos da **PRF** (sinistros 2025) e da **ANTT** (volumetria das praças de pedágio 2025) estejam no diretório raiz ou no caminho configurado nas células de ingestão do notebook.

### 2. Execução via Jupyter Notebook / VS Code
1. Inicie o servidor Jupyter ou abra o arquivo `.ipynb` diretamente no VS Code:
   ```bash
   jupyter notebook
   ```
2. Execute todas as células sequencialmente (**Run All**) para reproduzir a limpeza de dados, o treinamento dos modelos e a renderização dos mapas e dashboards interativos.

### 3. Execução via Google Colab
1. Faça o upload do arquivo `.ipynb` para o Google Colab.
2. Carregue as planilhas originais da PRF e da ANTT na aba de arquivos da sessão (`/content/`).
3. No menu superior, clique em **Ambiente de execução > Executar tudo**.

---

## O Que Foi Desenvolvido no Notebook

O fluxo analítico foi estruturado em 12 etapas reproduzíveis:

1. **Ingestão e Análise Exploratória (EDA):** Inspeção das bases da PRF e ANTT, análise de distribuição por municípios, condições climáticas e redução de dimensionalidade da variável `tracado_via` (de 605 variações textuais para 4 categorias estruturais).
2. **Cruzamento Relacional (`Merge`) e Saneamento Espacial:** Integração entre sinistros e fluxo diário de pedágios pela chave temporal (`datetime64[ns]`), além da correção de coordenadas geográficas distorcidas (outliers) por imputação de medianas em blocos de 10 km, gerando mapas de calor animados em janelas de 30 minutos com **Folium**.
3. **Delimitação de Escopo e Engenharia de KPI:** Filtragem estrita para o corredor **SP/PR** (4.170 ocorrências e 8.290 veículos afetados) e criação do indicador composto **Índice de Severidade** (`Peso da Gravidade x Número de Veículos`), segmentado nas classes de risco *Baixo*, *Médio* e *Alto*.
4. **Pré-processamento e Modelagem Preditiva:** Codificação de variáveis categóricas via *One-Hot Encoding*, padronização de escala (`StandardScaler`) e validação comparativa em conjuntos de treino e teste (80%/20%) entre **Redes Neurais Artificiais (MLP com TensorFlow/Keras)** e **Random Forest (Scikit-Learn)** para:
   * **Regressão:** Estimativa do volume diário de veículos na via.
   * **Classificação:** Previsão do nível de severidade operacional dos acidentes (58,11% de exatidão com Rede Neural contra 55,97% com Random Forest).
5. **Simulação Operacional e Dashboards Executivos:** Inferência dos modelos treinados em um cenário simulado de 50 km no trecho crítico do **KM 335 (Serra do Cafezal)** ao longo das 24 horas do dia, comparando condições de *Céu Claro* e *Chuva* para estimar atrasos de viagem (+26,9 min no pico chuvoso às 09h) e consolidando os resultados em painéis interativos com **Plotly**.
6. **Governança e LGPD:** Documentação de vieses de subnotificação, limitações de granularidade e conformidade com a Lei Geral de Proteção de Dados (Lei nº 13.709/2018), utilizando exclusivamente dados públicos anonimizados na origem.

---

## Competências e Tecnologias Utilizadas

* **Linguagem:** Python
* **Manipulação e Engenharia de Dados:** Pandas, NumPy
* **Machine Learning e Deep Learning:** Scikit-Learn (Random Forest, StandardScaler, LabelEncoder, métricas de avaliação) e TensorFlow/Keras (Redes Neurais Multilayer Perceptron para Regressão e Classificação Multiclasse)
* **Visualização de Dados e Geoprocessamento:** Plotly (Dashboards executivos e operacionais interativos), Folium (HeatMapWithTime), Seaborn e Matplotlib
* **Persistência de Modelos:** Joblib e formato nativo `.keras`

---

## Estrutura dos Entregáveis

* `*.ipynb` — Notebook principal executado com código comentado, análises estatísticas e visualizações interativas.
* `dicionario_dados_br116.pdf` — Documentação técnica das variáveis utilizadas, tipos de dados, origens e unidades de medida.
* `sintese_executiva_br116.pdf` — Resumo gerencial com a pergunta de negócio, resultados dos modelos, simulações e recomendações operacionais.
