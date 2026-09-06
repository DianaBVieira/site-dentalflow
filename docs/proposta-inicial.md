# DentalFlow — proposta inicial da nova versão

## 1. Objetivo do aplicativo

Criar uma plataforma de gestão e relacionamento para clínicas odontológicas que automatize a agenda sem perder o controle humano. O DentalFlow deve ajudar a clínica a responder pacientes, ocupar melhor os horários, reduzir faltas, organizar o histórico de relacionamento e transformar consultas em um fluxo operacional claro.

## 2. Público

### Principal

- Clínicas odontológicas pequenas e médias.
- Dentistas autônomos com recepção própria ou compartilhada.
- Recepcionistas responsáveis por agenda, confirmações e retornos.
- Gestores que acompanham ocupação, pacientes e resultados.

### Futuro

- Redes com várias unidades.
- Pacientes, por meio de um portal simples para confirmar horários, documentos e pagamentos.

## 3. Proposta de valor

“Da primeira mensagem ao retorno do paciente, toda a jornada organizada em um só fluxo.”

O produto deve combinar:

- Atendimento automatizado e transparente.
- Agenda confiável por profissional e unidade.
- CRM odontológico orientado a retorno e prevenção.
- Visão simples da operação e dos resultados.
- Segurança compatível com dados pessoais e de saúde.

## 4. Escopo recomendado para o MVP

### Fundação

- Cadastro de clínica, unidade, equipe e profissionais.
- Login seguro e perfis: administrador, dentista, recepção e financeiro.
- Permissões detalhadas e registro de ações importantes.
- Ambiente de demonstração completamente separado e com dados fictícios.

### Agenda

- Visões diária e semanal por profissional.
- Horários de trabalho, pausas, bloqueios, feriados e intervalo técnico.
- Criação manual ou originada por conversa.
- Estados: pendente, agendada, confirmada, em atendimento, concluída, cancelada, reagendada e falta.
- Prevenção de choque de horários no servidor.
- Sincronização opcional e segura com Google Calendar.

### Pacientes e CRM

- Cadastro, busca, contatos e preferências de comunicação.
- Histórico de consultas e interações.
- Consentimentos versionados com finalidade e revogação.
- Segmentos: novos, ativos, faltosos, inativos e manutenção ortodôntica.
- Lista de retornos e campanhas com aprovação humana antes do envio.

### Serviços

- Procedimentos com duração, intervalo técnico, preço-base e profissionais habilitados.
- Regras por unidade e profissional.
- Ativação/inativação sem apagar o histórico.

### Conversas e automações

- Integração oficial com WhatsApp Business por meio do servidor.
- Assistente identificado claramente como assistente virtual da clínica.
- Consulta de disponibilidade, agendamento, confirmação, reagendamento e cancelamento.
- Transferência imediata para atendimento humano.
- Lembretes configuráveis e controle de opt-out.
- Histórico de mensagens com retenção e acesso controlados.

### Painel

- Agenda e pendências do dia.
- Taxas de confirmação, falta, cancelamento e reagendamento.
- Ocupação por profissional.
- Origem dos agendamentos e tempo médio de resposta.
- Receita potencial separada de receita efetivamente recebida.

## 5. Fora do MVP

- Prontuário clínico completo e odontograma.
- Diagnóstico ou recomendação clínica por IA.
- Estoque completo.
- Contabilidade, emissão fiscal e conciliação bancária.
- Convênios complexos.
- Aplicativo nativo para celular.

Essas áreas podem ser planejadas desde já no modelo, mas não devem atrasar a validação do fluxo principal.

## 6. Estrutura de navegação

```text
DentalFlow
├── Hoje
│   ├── Agenda
│   ├── Confirmações
│   └── Pendências
├── Agenda
│   ├── Dia
│   ├── Semana
│   ├── Profissionais
│   └── Bloqueios
├── Pacientes
│   ├── Todos
│   ├── Perfil e histórico
│   ├── Retornos
│   └── Segmentos
├── Conversas
│   ├── Caixa de entrada
│   ├── Atendimento humano
│   └── Automações
├── Serviços
├── Campanhas
├── Relatórios
└── Configurações
    ├── Clínica e unidades
    ├── Equipe e permissões
    ├── Agenda e serviços
    ├── Canais e integrações
    ├── Privacidade
    └── Auditoria
```

## 7. Jornada central

1. O paciente envia uma mensagem.
2. O assistente se identifica, entende a intenção e apresenta o aviso de privacidade necessário.
3. O paciente escolhe serviço, profissional ou preferência de horário.
4. O servidor calcula opções realmente disponíveis.
5. O paciente confirma; o sistema cria a consulta e registra a origem.
6. A clínica acompanha a conversa e pode assumir a qualquer momento.
7. O sistema envia lembretes e recebe confirmação, reagendamento ou cancelamento.
8. Após a consulta, a equipe registra o resultado operacional e programa o retorno.
9. Pacientes elegíveis entram em listas de reativação revisadas pela equipe.

## 8. Estrutura técnica inicial

Começar como aplicação web responsiva. Ela atende a recepção no computador e permite uso em tablet ou celular sem multiplicar a complexidade do primeiro lançamento.

```text
APP_DentalFlow/
├── apps/
│   ├── web/                    # Interface administrativa
│   └── api/                    # API, autenticação e regras de negócio
├── packages/
│   ├── ui/                     # Design system DentalFlow
│   ├── domain/                 # Agenda, pacientes, conversas e serviços
│   ├── validation/             # Esquemas de entrada e saída
│   └── config/                 # Configuração compartilhada sem segredos
├── workers/
│   ├── notifications/          # Lembretes e campanhas
│   └── integrations/           # WhatsApp e calendários
├── database/
│   ├── migrations/
│   ├── policies/
│   └── seeds/                  # Somente dados fictícios
├── docs/
│   ├── produto/
│   ├── segurança/
│   └── decisoes/
└── tests/
    ├── acceptance/
    ├── integration/
    └── security/
```

### Módulos de domínio

- Organizações: clínica, unidade, usuário, profissional, função e permissão.
- Agenda: disponibilidade, recurso/cadeira, bloqueio, consulta e histórico de estados.
- Pacientes: cadastro, contato, preferências, consentimento e histórico.
- Catálogo: serviço, duração, intervalo, preço-base e habilitação profissional.
- Comunicação: conversa, mensagem, canal, modelo, opt-out e transferência humana.
- Automação: regra, execução, aprovação, tentativa e falha.
- Gestão: indicador, evento de auditoria e exportação.

Todas as informações operacionais devem pertencer explicitamente a uma clínica. O isolamento deve ser garantido no banco e na API, não apenas na interface.

## 9. Requisitos de segurança e LGPD

- Nenhuma credencial de WhatsApp, Google ou IA no navegador.
- Autenticação e autorização obrigatórias em cada rota do servidor.
- Permissões por clínica, unidade e função.
- Criptografia em trânsito e em armazenamento.
- Tokens de integração em cofre de segredos, com rotação e revogação.
- Auditoria para acesso e alteração de informações sensíveis.
- Consentimento com versão, finalidade, data, canal e revogação.
- Minimização de dados enviados a serviços de IA.
- Proibição de decisão ou orientação clínica autônoma por IA.
- Política de retenção, exportação e exclusão definida antes do piloto real.
- Backups com restauração testada.
- Dados fictícios em desenvolvimento, testes e demonstração.

## 10. Direção visual

### Preservar

- Verde como cor de confiança e cuidado.
- Base clara em creme e areia.
- Dente + conversa como conceito do símbolo.
- Interface objetiva, com menu lateral e cartões de leitura rápida.

### Evoluir

- Símbolo vetorial simples, sem efeitos tridimensionais.
- Nome visual “DentalFlow”, sem `@`.
- Paleta com contraste validado para acessibilidade.
- Componentes com estados consistentes: normal, foco, carregando, sucesso, alerta e erro.
- Fotografia e ilustrações que representem clínicas brasileiras reais e diversas.
- Tom acolhedor, direto e transparente sobre automações.

Paleta inicial a validar:

- Verde principal: evolução do verde sálvia existente.
- Verde escuro: navegação, títulos e contraste.
- Creme: fundo principal.
- Areia: divisórias e superfícies secundárias.
- Verde vivo: ações e confirmações, usado com moderação.
- Âmbar e vermelho: alertas, faltas e erros, nunca apenas por cor.

## 11. Indicadores de sucesso

- Tempo para concluir um agendamento.
- Percentual de conversas resolvidas sem retrabalho.
- Percentual de transferências para atendimento humano.
- Taxas de confirmação, falta, cancelamento e reagendamento.
- Ocupação da agenda por profissional.
- Pacientes reativados e retornos realizados.
- Incidentes de privacidade ou acesso indevido: meta zero.
- Satisfação de recepção e dentistas no piloto.

## 12. Fases sugeridas

### Fase 1 — validação

- Entrevistar dentista, recepção e gestor.
- Validar vocabulário, regras de agenda e prioridades.
- Definir se o primeiro piloto terá uma ou várias unidades.

### Fase 2 — protótipo

- Criar fluxo navegável de conversa, agenda, paciente e retorno.
- Testar com dados fictícios e cenários de exceção.

### Fase 3 — fundação

- Implementar organizações, equipe, permissões, auditoria e ambientes separados.
- Configurar banco, segredos, observabilidade e backups.

### Fase 4 — MVP

- Entregar agenda, pacientes, serviços, conversas, automações e painel.
- Integrar WhatsApp e Google Calendar em ambiente de teste.

### Fase 5 — piloto controlado

- Operar com uma clínica parceira.
- Importar dados apenas após ensaio em cópia e autorização explícita.
- Medir resultados, corrigir falhas e testar recuperação.

### Fase 6 — expansão

- Abrir novas clínicas gradualmente.
- Priorizar prontuário, odontograma ou financeiro completo conforme evidência do piloto.

## 13. Decisões pendentes antes de programar

1. O primeiro cliente será uma clínica específica ou o produto já nascerá comercial para várias clínicas?
2. Quantos profissionais, unidades e cadeiras precisam ser suportados no piloto?
3. O WhatsApp será o canal principal desde o primeiro teste real?
4. Quem aprova campanhas e mensagens automáticas?
5. Qual é o limite entre cadastro operacional e prontuário clínico no MVP?
6. Quais dados da versão atual precisam ser preservados ou migrados?
7. A marca será redesenhada agora ou após a validação do protótipo?

Nenhuma migração, publicação ou uso de dados reais deve ocorrer sem autorização explícita.
