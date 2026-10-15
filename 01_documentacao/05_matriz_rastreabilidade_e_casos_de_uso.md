# Matriz de Rastreabilidade e Casos de Uso

## 1. Matriz de Rastreabilidade (MoSCoW)

A matriz abaixo correlaciona os requisitos funcionais aos casos de uso operacionais e módulos da plataforma, categorizados pela metodologia **MoSCoW** (*Must have, Should have, Could have, Won't have* para MVP):

| ID Requisito | Descrição Resumida | Módulo Responsável | Caso de Uso | Prioridade |
| :--- | :--- | :--- | :--- | :---: |
| **RF01** | Captura Digital e OCR de Notas/Cupons | Despesas | UC01 | **Must** |
| **RF02** | Agrupamento em Relatório de Despesas | Despesas | UC01, UC06 | **Must** |
| **RF03** | Cálculo de KM com Rotas por GPS | Despesas | UC02 | **Must** |
| **RF04** | Gestão e Dedução de Adiantamentos | Despesas / Financeiro | UC03 | **Must** |
| **RF05** | Rateio Multi-centro de Custo / Projetos | Despesas / Governança | UC01, UC08 | **Must** |
| **RF06** | Conversão Multi-moeda de Despesas | Despesas | UC01 | **Should** |
| **RF07** | Busca e Emissão de Voos via GDS | Viagens (OBT) | UC04 | **Must** |
| **RF08** | Reserva de Hotéis com Teto de Diária | Viagens (OBT) | UC04 | **Must** |
| **RF09** | Locação de Automóveis Homologada | Viagens (OBT) | UC04 | **Should** |
| **RF10** | Gestão de Grupos e Eventos Corporativos | Viagens (OBT) | UC04 | **Could** |
| **RF11** | Gestão de Bilhetes Não Voados (Créditos) | Viagens (OBT) | UC04 | **Should** |
| **RF12** | Emissão de Cartão Físico e Virtual | Cartões & Pagamentos | UC05 | **Must** |
| **RF13** | Conciliação em Tempo Real de Comprovantes | Cartões & Pagamentos | UC05 | **Must** |
| **RF14** | Fundo Fixo com Limites Parametrizáveis | Cartões & Pagamentos | UC10 | **Must** |
| **RF15** | Pagamentos e Reembolsos via Pix | Cartões & Pagamentos | UC03, UC08 | **Should** |
| **RF16** | Alçadas Multinível e Aprovação por Exceção | Governança | UC06 | **Must** |
| **RF17** | Aprovação por App e Dispositivos Móveis | Governança / Mobile | UC06 | **Must** |
| **RF18** | Delegação Temporária de Alçada (Férias) | Governança | UC06 | **Should** |
| **RF19** | Auditoria Preditiva de Fraudes com IA | Inteligência Artificial | UC07 | **Must** |
| **RF20** | Assistente Conversacional TEO | Inteligência Artificial | UC01, UC04 | **Should** |
| **RF21** | Sincronização de Usuários e Centros de Custo | Integrações / ERP | UC08 | **Must** |
| **RF22** | Envio de Contas a Pagar ao ERP | Integrações / ERP | UC08 | **Must** |
| **RF23** | Geração e Leitura de Arquivo CNAB 240/400 | Integrações / Bancos | UC08 | **Should** |

---

## 2. Casos de Uso Detalhados (UC)

### UC01: Lançar Despesa com OCR via Aplicativo Móvel
- **Ator Principal**: Colaborador / Viajante.
- **Pré-condições**: Usuário autenticado no app móvel com acesso à câmera.
- **Fluxo Principal**:
  1. O colaborador acessa o app e clica em **"Nova Despesa"**.
  2. O colaborador fotografa o cupom fiscal (ou faz upload do arquivo PDF/imagem).
  3. O serviço de OCR processa o documento, extrai os metadados (Data, Valor, Estabelecimento, CNPJ, Itens) e pré-preenche o formulário.
  4. O colaborador seleciona a categoria da despesa (ex: Alimentação) e o centro de custo/projeto.
  5. O colaborador clica em **"Salvar e Adicionar ao Relatório"**.
  6. O sistema confirma o armazenamento e atualiza o totalizador do relatório de despesas.
- **Fluxos Alternativos**:
  - *3a. Imagem ilegível ou sem QR Code*: O sistema emite alerta solicitando que o usuário digite manualmente os dados obrigatórios e reforce a foto.

---

### UC02: Solicitação e Liquidação de Reembolso de KM
- **Ator Principal**: Colaborador em deslocamento externo.
- **Pré-condições**: Veículo particular cadastrado e valor do KM fixado na política da empresa.
- **Fluxo Principal**:
  1. O colaborador seleciona a opção **"Reembolso de KM"**.
  2. O colaborador informa o ponto de saída (ex: Residência ou Escritório), os pontos de visita/clientes e o ponto de chegada.
  3. O sistema calcula a menor rota viável via Google Maps e apresenta a distância total em KM.
  4. O sistema aplica o desconto do trajeto habitual de ida e volta ao trabalho (conforme RN04).
  5. O sistema multiplica a distância líquida pela tarifa configurada (ex: 180 km * R$ 1,20 = R$ 216,00).
  6. O colaborador adiciona a justificativa da viagem e anexa a despesa ao seu relatório.

---

### UC03: Solicitação e Prestação de Contas de Adiantamento
- **Atores**: Colaborador, Gestor Aprovador e Contas a Pagar.
- **Fluxo Principal**:
  1. O colaborador abre uma **"Solicitação de Adiantamento"** informando o motivo, a data estimada da viagem e o valor necessário (ex: R$ 1.500,00).
  2. O gestor recebe a notificação e aprova o adiantamento.
  3. A solicitação é enviada ao ERP/Banco para liquidação (via Pix ou TED).
  4. Após a viagem, o colaborador cria um relatório de prestação de contas com comprovantes somando R$ 1.300,00.
  5. O sistema deduz automaticamente o valor do saldo adiantado:
     - Saldo devedor pelo colaborador à empresa: R$ 200,00.
  6. O sistema gera uma chave Pix ou boleto de cobrança para que o colaborador devolva os R$ 200,00 não utilizados.
  7. Com o comprovante de devolução anexado, o relatório é encerrado e contabilizado no ERP.

---

### UC04: Emissão de Passagem Aérea e Hotel com Regra de Antecedência
- **Atores**: Colaborador / Viajante, Gestor Imediato, Diretor (se exceção).
- **Fluxo Principal**:
  1. O viajante acessa o módulo de viagens e pesquisa voos de ida e volta (São Paulo -> Recife).
  2. A data da viagem solicitada é para daqui a 5 dias (a política da empresa exige no mínimo 10 dias).
  3. O sistema exibe o aviso de **Violação de Política (Antecedência Crítica)**.
  4. O viajante seleciona o voo mais econômico da lista e é obrigado a preencher uma justificativa detalhada para a urgência da viagem.
  5. A solicitação é encaminhada para aprovação do Gestor Imediato e escalada automaticamente para o Diretor da área (alçada por exceção).
  6. O Diretor aprova a solicitação com base na justificativa.
  7. O bilhete aéreo é emitido imediatamente no GDS e o voucher enviado para o app do colaborador.

---

### UC05: Transação com Cartão Corporativo e Conciliação Instantânea
- **Atores**: Portador do Cartão, Adquirente/Bandeira, Motor Paytrack.
- **Fluxo Principal**:
  1. O colaborador efetua o pagamento de um almoço corporativo de R$ 95,00 utilizando o Cartão Corporativo Paytrack.
  2. O adquirente envia o webhook de autorização em tempo real para a Paytrack.
  3. O motor Paytrack verifica:
     - Saldo e limite disponível: OK.
     - Código de Categoria do Estabelecimento (MCC 5812 - Restaurantes): Autorizado.
  4. A transação é autorizada na maquininha.
  5. Uma notificação push chega instantaneamente no celular do colaborador: *"Você gastou R$ 95,00 no Restaurante X. Fotografe a nota fiscal agora para conciliar."*
  6. O colaborador clica no push, tira a foto do comprovante e o sistema realiza o pareamento automático e a conciliação da fatura.

---

### UC06: Aprovação Multinível e Delegação de Alçada
- **Atores**: Gestor Aprovador, Gestor Delegado.
- **Fluxo Principal**:
  1. Um gestor programa suas férias no sistema de 01/11 a 15/11 e delega sua alçada de aprovação para outro gestor de mesmo nível.
  2. Um colaborador submete um relatório de despesas de R$ 4.500,00 durante o período.
  3. O sistema direciona a solicitação automaticamente para a caixa de entrada do gestor delegado.
  4. O gestor delegado avalia os comprovantes, as categorias e eventuais alertas do motor de IA.
  5. O gestor delegado clica em **"Aprovar"**.
  6. O sistema registra na trilha de auditoria: *"Aprovado por Gestor Delegado B em substituição temporária a Gestor A"*.

---

### UC07: Auditoria Preditiva de Despesas com Inteligência Artificial
- **Atores**: Motor de Inteligência Artificial Paytrack, Auditor Financeiro.
- **Fluxo Principal**:
  1. Durante a submissão de um relatório, o motor de IA executa uma bateria de verificações automáticas:
     - Checagem de duplicação: compara chave fiscal e hash visual da nota com a base histórica.
     - Validação de itens: analisa texto extraído buscando termos não permitidos (cerveja, vinho, cigarros).
     - Razoabilidade de valor: compara valor da refeição com a média praticada na região.
  2. O sistema detecta que o mesmo cupom fiscal de combustível foi anexado em outro relatório há 30 dias.
  3. O sistema aplica a tag **[ALERTA_DUPLICIDADE_CRITICA]** e bloqueia o avanço automático para pagamento.
  4. A equipe de auditoria financeira recebe a ocorrência em sua fila prioritária de conformidade para análise manual e abertura de processo de esclarecimento.

---

### UC08: Integração Automática com Contas a Pagar do ERP
- **Atores**: Motor de Integrações Paytrack, ERP Corporativo (SAP/TOTVS/etc).
- **Fluxo Principal**:
  1. Um relatório de despesas recebe a aprovação financeira final.
  2. O evento de webhook `expense_report.approved` é disparado internamente.
  3. O conector Paytrack formata o payload contábil de acordo com o plano de contas e centro de custo configurado para o cliente.
  4. O conector realiza a chamada REST autenticada contra o endpoint do ERP da empresa enviando o `Idempotency-Key`.
  5. O ERP cria o título a pagar (fornecedor/colaborador, valor líquido, vencimento e dados bancários/Pix).
  6. O ERP responde com HTTP `200` contendo o número do documento contábil gerado (`DOC-ERP-XXXX`).
  7. A Paytrack grava o identificador do ERP no relatório, garantindo rastreabilidade contábil completa de ponta a ponta.
