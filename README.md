
# 🎯 Radar B2B - Inteligência de Mercado

Aplicativo móvel desenvolvido com **React Native (Expo)** para identificar oportunidades estratégicas ("Oceanos Azuis") para abertura de agências de Análise de Dados e B.I. no Brasil.

O app cruza dados econômicos, populacionais e de concorrência para listar as melhores cidades e fornece uma lista de leads qualificados (Top 600 empresas por faturamento) para prospecção ativa.

---

## 🚀 Funcionalidades Principais

-   **Mapa de Oportunidades:** Ranqueamento de cidades baseado em Score proprietário (PIB, Concorrência, Volume Bancário).
-   **Leads Offline:** Banco de dados SQLite embarcado com +600 empresas por cidade.
-   **Download Inteligente:** Arquitetura "Download on First Launch" para baixar o banco de dados (600MB+) via GitHub Releases na primeira execução, mantendo o APK leve (~30MB).
-   **Filtros Avançados:** Filtragem por Nível de Concorrência (Oceano Azul, Alta, Média), População, Região e Nicho (Agro, Indústria, Serviços).
-   **Ações Diretas:**
    -   📞 Ligar diretamente para a empresa.
    -   📧 Enviar E-mail (com validação de e-mails nulos/inválidos).
    -   📍 Copiar endereço completo para GPS.
-   **Busca Híbrida:** Algoritmo de busca que resolve problemas de acentuação (ex: encontra "Querência" buscando por "QUERENCIA").

---

## 🛠️ Tecnologias Utilizadas

-   **Core:** React Native, Expo Go (SDK 50+).
-   **Banco de Dados:** SQLite (`expo-sqlite` New Async API).
-   **Gerenciamento de Arquivos:** `expo-file-system/legacy` (Download e Persistência).
-   **Navegação:** React Navigation (Stack).
-   **UI/UX:** `react-native-safe-area-context`, `expo-vector-icons`.
-   **Utils:** `expo-clipboard`, `expo-asset`.

---

## 🏗️ Arquitetura do Projeto

O projeto utiliza uma arquitetura otimizada para lidar com grandes volumes de dados sem exceder os limites das lojas de aplicativos:

1.  **APK Leve:** O aplicativo é instalado sem o banco de dados principal.
2.  **Bootstrap:** Ao abrir, o `database.js` verifica a existência do banco.
3.  **Download:** Se não existir, baixa o arquivo `.db` (hospedado no GitHub Releases) direto para o diretório do sistema.
4.  **Conexão Global:** O `SQLiteProvider` no `App.js` mantém a conexão aberta para alta performance nas consultas.

### Estrutura de Pastas

```bash
/
├── assets/             # Imagens e ícones
├── App.js              # Entrada, Provider SQLite e Lógica de Download
├── database.js         # Script de gerenciamento do arquivo .db
├── dados.js            # JSON leve com metadados das 5570 cidades
├── HomeScreen.js       # Dashboard, Filtros e Lista de Cidades
└── ListaClientes.js    # Lista de Leads (FlatList Otimizada) e Consultas SQL
