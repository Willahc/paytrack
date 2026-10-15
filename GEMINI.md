# Diretrizes e Padrão de Pesquisa do Workspace Paytrack

Este repositório estabelece o padrão corporativo de pesquisa aprofundada, inteligência de negócios, levantamento de requisitos e engenharia de software para análise de empresas e plataformas.

---

## 📌 Protocolo Padrão para Próximas Pesquisas
Sempre que uma nova empresa, produto, plataforma, concorrente ou parceiro for submetido para pesquisa neste ambiente, o assistente deve aplicar o **Protocolo de Inteligência 360°** formalizado em [`01_documentacao/08_metodologia_padrao_pesquisa_empresas.md`](file:///C:/Users/kbadmin/Documents/Projetos/Mobilidade%20e%20Viagens/Paytrack/01_documentacao/08_metodologia_padrao_pesquisa_empresas.md):

### 1. Varredura Técnica e Arquitetura de Software
- Componentes de sistema (Frontend, Backend, APIs, Barramento, Segurança).
- Módulos operacionais e fluxos de dados ponta a ponta.
- Recursos de inteligência artificial, automação e integrações de terceiros.

### 2. Engenharia de Requisitos e Regras de Negócio
- Personas corporativas e atores do sistema.
- Requisitos Funcionais (**RF**), Não Funcionais (**RNF**) e Regras de Negócio Críticas (**RN**).
- Matriz de Rastreabilidade **MoSCoW** e Casos de Uso detalhados (**UC**).

### 3. Integrações e Especificação de APIs
- Protocolos de autenticação (OAuth 2.0 / API Keys), headers de idempotência e rate limits.
- Modelagem de dados (diagramas ER).
- Payloads JSON reais de requisição e resposta para endpoints essenciais.
- Catálogo de Webhooks e conectores nativos de ERPs (SAP, TOTVS, Senior, Sankhya).

### 4. Inteligência Institucional e Finanças
- Ano de fundação, polo de tecnologia de origem, sede e escritórios regionais.
- Fundadores e diretoria executiva atual (trajetória e papéis).
- Histórico de investimentos: rodadas (Seed, Série A, Série B), fundos líderes e valores aportados.
- Métricas de escala: total de clientes, usuários ativos e número de colaboradores.
- Carteira de clientes de referência agrupada por segmento.

### 5. Go-to-Market (GTM), ICP e Diferenciais Competitivos
- Perfil de Cliente Ideal (**ICP**): faturamento, porte de funcionários, gastos mensais e ERP instalado.
- Comitê de Compra (*Buying Center*): dores e discursos de valor para CFO, Gestor de Viagens e TI.
- Canais de Aquisição de Clientes (Inbound com calculadoras/ferramentas, Outbound/ABM, Programas de Indicação B2B, Parcerias de ERP e Eventos).
- Matriz de Posicionamento Competitivo (*quadrantChart*) e análise do *Moat* (fosso defensivo).

---

## 📂 Organização e Padrão de Arquivos
- Preservar a estrutura de pastas em conformidade com [`INDICE_PROJETOS.md`](file:///C:/Users/kbadmin/Documents/Projetos/INDICE_PROJETOS.md):
  - Documentação sempre em `01_documentacao/`.
  - Índice executivo sempre atualizado em `README.md`.
  - Arquivos numerados progressivamente (`01_*` a `08_*`).
  - Utilizar diagramas Mermaid em todas as análises para máxima clareza visual.
  - Manter sempre links clicáveis em padrão `file://`.
