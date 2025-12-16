# 🎯 Radar B2B - Inteligência de Mercado & Oceano Azul

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=FINALIZADO&color=GREEN&style=for-the-badge)
![Badge React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Badge Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)
![Badge BigQuery](https://img.shields.io/badge/Google_BigQuery-669DF6?style=for-the-badge&logo=googlebigquery&logoColor=white)
![Badge SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

> **Uma ferramenta estratégica para identificar cidades brasileiras com alto potencial econômico e baixa concorrência para abertura de Agências de Dados e B.I.**

---

## 🖼️ Screenshots

| Dashboard Principal | Menu de Filtros | Detalhes & Leads |
|:---:|:---:|:---:|
| ![Dashboard](https://via.placeholder.com/200x400?text=Dashboard+App) | ![Filtros](https://via.placeholder.com/200x400?text=Filtros+Laterais) | ![Detalhes](https://via.placeholder.com/200x400?text=Lista+de+Leads) |

---

## 💡 Sobre o Projeto

O **Radar B2B** não é apenas um catálogo de cidades. É uma aplicação de **Business Intelligence** que cruza dados massivos de fontes públicas para responder a uma pergunta de negócio crítica:

> *"Onde eu devo abrir minha empresa de Análise de Dados para encontrar clientes ricos e fugir da concorrência?"*

O app classifica mais de 5.500 cidades brasileiras utilizando algoritmos de pontuação que equilibram **Riqueza (PIB/Bancos)** com **Saturação de Mercado (Concorrência)**, e fornece uma lista de prospecção com as **600 maiores empresas** de cada município.

---

## 🚀 Funcionalidades

### 🧠 Inteligência de Mercado
-   **🔍 Busca Híbrida Inteligente:** Pesquisa instantânea que resolve problemas de acentuação (ex: encontra "Querência" buscando "QUERENCIA").
-   **🌊 Indicador "Oceano Azul":** Identifica automaticamente cidades com alta demanda (empresas ativas) e ZERO concorrência registrada.
-   **📊 Score de Oportunidade:** Um ranking calculado matematicamente que prioriza cidades ricas e desassistidas.
-   **📍 Filtros Avançados:** Filtragem por Estado (UF), População, Nicho (Agro/Serviços/Indústria) e Nível de Concorrência.

### 💼 CRM & Prospecção (Novidades v2.0)
-   **📂 Leads Offline:** Banco de dados embarcado com as **Top 600 empresas** por faturamento de cada cidade.
-   **📞 Ação Direta:** Botões para ligar, copiar endereço e enviar e-mail diretamente pelo app.
-   **🛡️ Validação de Dados:** O sistema de e-mail possui validação automática, ocultando o botão caso a empresa não tenha e-mail cadastrado na Receita.

---

## 🏗️ Arquitetura Técnica (Download on First Launch)

Um dos maiores desafios técnicos deste projeto foi disponibilizar um banco de dados massivo (**+3 milhões de empresas, ~600MB**) em um aplicativo móvel sem exceder os limites da Play Store/App Store.

**A Solução:**
1.  **APK Leve:** O aplicativo é compilado e instalado com apenas ~30MB.
2.  **Hospedagem Externa:** O banco de dados SQLite (`.db`) é hospedado no **GitHub Releases**.
3.  **Bootstrap Inteligente:** Ao abrir o app pela primeira vez, o script `database.js` baixa o banco de dados via Wi-Fi e o instala na pasta do sistema (`FileSystem`).
4.  **Performance:** Utilizamos `SQLiteProvider` para manter uma conexão global única, evitando vazamento de memória e garantindo consultas instantâneas mesmo com milhões de linhas.

---

## 🧠 A Metodologia (Data Science)

O pipeline de dados foi construído para garantir precisão estratégica:

### 1. Extração & Big Data (SQL + BigQuery)
Utilizamos o **Google BigQuery** e a biblioteca `basedosdados` para cruzar tabelas governamentais:
* **Dados Financeiros:** PIB (IBGE) e Volume Bancário (Banco Central).
* **Empresas Ativas:** Contagem de CNPJs ativos (exceto MEI) para medir tamanho do mercado.
* **Concorrência:** Filtragem de CNPJs com CNAEs de T.I. (62.0), Tratamento de Dados (63.1) e Consultoria (70.2).

### 2. Algoritmo de Pontuação (Python)
No Python (Pandas), criamos o **Score de Oportunidade**:
```python
Score = (Rank_Riqueza * 0.5) + (Rank_Demanda * 0.5) * Fator_Concorrencia


