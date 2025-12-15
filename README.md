# 🎯 Radar B2B - Inteligência de Mercado & Oceano Azul

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)
![Badge React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Badge Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)
![Badge BigQuery](https://img.shields.io/badge/Google_BigQuery-669DF6?style=for-the-badge&logo=googlebigquery&logoColor=white)

> **Uma ferramenta estratégica para identificar cidades brasileiras com alto potencial econômico e baixa concorrência para abertura de Agências de Dados e B.I.**

---

## 🖼️ Screenshots

| Dashboard Principal | Menu de Filtros | Detalhes da Cidade |
|:---:|:---:|:---:|
| ![Dashboard](https://via.placeholder.com/200x400?text=Dashboard+App) | ![Filtros](https://via.placeholder.com/200x400?text=Filtros+Laterais) | ![Detalhes](https://via.placeholder.com/200x400?text=Analise+Cidade) |


---

## 💡 Sobre o Projeto

O **Radar B2B** não é apenas um catálogo de cidades. É uma aplicação de **Business Intelligence** que cruza dados massivos de fontes públicas para responder a uma pergunta de negócio crítica:

> *"Onde eu devo abrir minha empresa de Análise de Dados para encontrar clientes ricos e fugir da concorrência?"*

O app classifica mais de 5.000 cidades brasileiras utilizando algoritmos de pontuação que equilibram **Riqueza (PIB/Bancos)** com **Saturação de Mercado (Concorrência)**.

---

## 🚀 Funcionalidades

-   **🔍 Busca Inteligente:** Pesquisa instantânea de qualquer cidade do Brasil.
-   **🌊 Indicador "Oceano Azul":** Identifica automaticamente cidades com alta demanda (empresas ativas) e ZERO concorrência registrada.
-   **📊 Score de Oportunidade:** Um ranking calculado matematicamente que prioriza cidades ricas e desassistidas.
-   **📍 Filtros Avançados:** Filtragem por Estado (UF), População, Nicho (Agro/Serviços/Indústria) e Nível de Concorrência.
-   **📈 KPI "Clientes por Agência":** Mostra a relação de oferta e demanda (Ex: 5.000 clientes potenciais para cada 1 agência).
-   **💎 Joias Raras:** Destaque para cidades menores, fora do radar, mas extremamente lucrativas.

---

## 🧠 A Metodologia (Data Science)

O diferencial deste projeto é o tratamento de dados realizado antes do app. O pipeline de dados foi construído da seguinte forma:

### 1. Extração & Big Data (SQL + BigQuery)
Utilizamos o **Google BigQuery** e a biblioteca `basedosdados` para cruzar tabelas gigantescas:
* **Dados Financeiros:** PIB (IBGE) e Volume Bancário (Banco Central).
* **Empresas Ativas (Demanda):** Contagem de CNPJs ativos (exceto MEI) na cidade.
* **Concorrência (Oferta):** Filtragem de CNPJs com CNAEs específicos de T.I. (62.0), Tratamento de Dados (63.1) e Consultoria (70.2).

### 2. Algoritmo de Pontuação (Python)
No Python (Pandas), criamos o **Score de Oportunidade**:
```python
Score = (Rank_Riqueza * 0.5) + (Rank_Demanda * 0.5) * Fator_Concorrencia
