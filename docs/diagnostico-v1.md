# Diagnóstico da primeira versão

## Referência analisada

- Repositório: `https://github.com/DianaBVieira/DentalFlow`
- Branch: `main`
- Commit analisado: `eda4cd06698ee0f5edaad13cd864edccd93aafca`
- Data do commit: 9 de julho de 2026
- Condição: análise somente de leitura

## Visão atual do produto

A primeira versão posiciona o DentalFlow como um sistema inteligente de agendamento odontológico via WhatsApp, acompanhado por um painel administrativo e CRM de pacientes. Ela já demonstra bem o núcleo da ideia: captar o pedido do paciente, localizar horários disponíveis, agendar, acompanhar a consulta e reativar pacientes.

## Estrutura existente

A solução atual é uma aplicação web em React e TypeScript, com interface construída em Vite e Tailwind. Há um servidor Express, autenticação Firebase, modelos de Firestore, integração inicial com Google Calendar e uso do Gemini no fluxo conversacional.

Principais áreas encontradas:

- Login com e-mail/senha ou Google.
- Painel com consultas, confirmações, faltas, cancelamentos, receita estimada e serviços realizados.
- Agenda diária com cadastro manual e alteração do estado da consulta.
- Cadastro de serviços, duração, intervalo técnico, preço e descrição.
- CRM de pacientes com histórico, consentimento, faltas e valor acumulado.
- Campanhas simuladas de reativação de pacientes inativos e manutenção ortodôntica.
- Configurações da clínica, horários, nome da assistente, instruções de IA, WhatsApp e Google Agenda.
- Assistente conversacional capaz de consultar disponibilidade, agendar e cancelar.

## Identidade existente

A primeira versão possui duas expressões visuais diferentes:

- Marca principal com dente dentro de um balão de conversa, reforçando odontologia + WhatsApp.
- Interface administrativa com verde sálvia, creme, areia e cinza-esverdeado.
- Tipografia de interface baseada em Inter, Space Grotesk e JetBrains Mono.
- Linguagem acolhedora e próxima, com forte presença de mensagens amigáveis.

### O que preservar

- O nome DentalFlow e a associação imediata com fluxo simples de atendimento.
- O dente e o balão de conversa como conceitos centrais da marca.
- A paleta acolhedora em verde, creme e tons naturais.
- A clareza do menu lateral e a leitura rápida dos indicadores.
- A automação de agenda por conversa como principal diferencial.
- A atenção a duração do procedimento e intervalo técnico entre consultas.
- Os estados claros da consulta e a visão de faltas/cancelamentos.
- O CRM de reativação e o acompanhamento de manutenção ortodôntica.

### O que melhorar na identidade

- Simplificar o logotipo para funcionar bem em tamanhos pequenos e fundos variados.
- Remover o efeito tridimensional e o uso de `@` no nome visual, preservando WhatsApp como integração, não como parte permanente da marca.
- Definir uma única linguagem visual entre login, painel, materiais comerciais e comunicações.
- Elevar contraste, tamanhos mínimos e estados de foco para acessibilidade.
- Tornar o texto acolhedor sem sugerir que uma IA é uma pessoa real.

## Limitações da primeira versão

### Produto

- A regra atual está fortemente ligada a uma única clínica e uma única profissional.
- Não há estrutura completa para múltiplas clínicas, unidades, cadeiras ou profissionais.
- O cadastro do paciente é reduzido e não equivale a prontuário clínico.
- Receita é estimada a partir da consulta, sem contas a receber, parcelas, pagamento ou conciliação.
- Campanhas e WhatsApp ainda funcionam principalmente como simulação.
- A agenda prioriza a visão diária e precisa evoluir para semana, profissional, unidade e recursos.

### Segurança e privacidade

- As rotas do servidor precisam validar autenticação e autorização em cada operação, não apenas esconder telas após o login.
- As regras atuais do Firestore permitem que qualquer usuário autenticado leia e escreva as coleções principais; faltam clínica, função e escopo.
- Credenciais de WhatsApp aparecem em formulário da interface. Segredos devem permanecer somente no servidor e em cofre próprio.
- Tokens do Google Calendar não devem ser tratados como dados comuns; precisam de armazenamento protegido, rotação e revogação.
- O consentimento LGPD atual é apenas uma data. É necessário registrar versão do termo, finalidade, canal, prova e eventual revogação.
- Informações pessoais aparecem duplicadas em consultas; isso aumenta inconsistências e exposição.
- O modo de teste precisa ser isolado de produção e usar somente dados fictícios.

### Engenharia

- O servidor concentra API, dados de demonstração, regras de agenda, IA e integrações em um único arquivo grande.
- O armazenamento local em arquivo não é adequado para uso real ou concorrente.
- Faltam validação de entrada, respostas de erro consistentes, paginação, observabilidade e testes automatizados.
- Regras importantes, textos e nomes estão fixos no código.
- A modelagem atual não possui clínica como chave obrigatória de isolamento.
- Há sinais de problemas de codificação de caracteres em alguns textos da interface.

## Direção recomendada

Preservar a primeira versão como prova do conceito de automação de agenda e relacionamento, mas reconstruir a fundação para operação real. A nova versão deve nascer multiclínica, com permissões por função, segredos no servidor, auditoria e um modelo de dados preparado para agenda, paciente, tratamento e financeiro.

O diferencial inicial não deve ser “ter todas as funções de um prontuário”. Deve ser executar muito bem o ciclo:

`conversa → consentimento → agendamento → confirmação → atendimento → retorno/reativação`.

Prontuário clínico completo, odontograma, assinatura e faturamento avançado podem entrar depois que esse ciclo estiver validado.
