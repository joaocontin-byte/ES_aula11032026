## UC01 — Realizar Login

**Ator Principal**
Usuário (Aluno, Recepcionista, Instrutor, Gerente)

**Objetivo**
Permitir que o usuário acesse o sistema com suas credenciais.

**Pré-condições**
- Usuário deve possuir cadastro ativo no sistema.

**Pós-condições**
- Sessão iniciada com sucesso e usuário redirecionado para a tela inicial de seu perfil.

**Fluxo Principal**
1. O usuário acessa a tela de login.
2. O usuário informa e-mail e senha.
3. O sistema valida as credenciais.
4. O sistema autentica o usuário e redireciona para a tela inicial correspondente ao seu perfil.

**Fluxos Alternativos**
- A1 — Senha incorreta: O sistema exibe mensagem de erro e solicita nova tentativa.
- A2 — Conta bloqueada por inadimplência: O sistema impede o login e exibe mensagem informando o bloqueio.
- A3 — Usuário não encontrado: O sistema exibe mensagem de erro informando que o cadastro não existe.

**RF Relacionados**
- RF04 — Regularidade do Aluno

**RNF Relacionados**
- RNF02 — Segurança
- RNF03 — Performance
- RNF04 — Usabilidade

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC02 — Cadastrar Aluno

**Ator Principal**
Recepcionista

**Objetivo**
Permitir o cadastro de novos alunos no sistema com todas as informações necessárias.

**Pré-condições**
- Recepcionista deve estar autenticado no sistema.
- Aluno não deve possuir cadastro ativo anterior.

**Pós-condições**
- Aluno cadastrado com sucesso e vinculado a um plano.

**Fluxo Principal**
1. A recepcionista acessa o módulo de cadastro de alunos.
2. A recepcionista preenche os dados pessoais, contato, endereço e plano contratado do aluno.
3. O sistema valida os dados informados.
4. O sistema registra o novo aluno.
5. O sistema confirma o cadastro e exibe os dados do aluno.

**Fluxos Alternativos**
- A1 — Dados incompletos: O sistema exibe mensagem indicando os campos obrigatórios não preenchidos.
- A2 — Aluno já cadastrado: O sistema exibe mensagem informando que o CPF ou e-mail já existe.

**RF Relacionados**
- RF01 — Cadastro de Alunos

**RNF Relacionados**
- RNF02 — Segurança
- RNF04 — Usabilidade

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC03 — Gerenciar Planos

**Ator Principal**
Gerente

**Objetivo**
Permitir que o gerente crie, edite, ative e desative planos disponíveis na academia.

**Pré-condições**
- Gerente deve estar autenticado no sistema.

**Pós-condições**
- Plano criado, editado, ativado ou desativado com sucesso.

**Fluxo Principal**
1. O gerente acessa o módulo de gerenciamento de planos.
2. O gerente seleciona a operação desejada: criar, editar, ativar ou desativar.
3. O gerente preenche ou altera os dados do plano (nome, valor, duração, modalidade).
4. O sistema valida as informações.
5. O sistema salva as alterações e confirma a operação.

**Fluxos Alternativos**
- A1 — Dados inválidos: O sistema exibe mensagem de erro e solicita correção.
- A2 — Plano vinculado a alunos ativos ao desativar: O sistema exibe aviso e solicita confirmação antes de prosseguir.

**RF Relacionados**
- RF02 — Gerenciamento de Planos

**RNF Relacionados**
- RNF04 — Usabilidade
- RNF05 — Escalabilidade

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC04 — Registrar Pagamento

**Ator Principal**
Recepcionista

**Objetivo**
Registrar o pagamento da mensalidade de um aluno e atualizar sua situação de regularidade.

**Pré-condições**
- Recepcionista deve estar autenticado.
- Aluno deve estar cadastrado no sistema.

**Pós-condições**
- Pagamento registrado e situação do aluno atualizada para regular.

**Fluxo Principal**
1. A recepcionista acessa o módulo de pagamentos.
2. A recepcionista localiza o aluno pelo nome ou CPF.
3. A recepcionista seleciona a forma de pagamento (dinheiro, cartão ou PIX).
4. O sistema registra o pagamento pelo valor integral.
5. O sistema atualiza imediatamente a situação do aluno para regular.
6. O sistema emite comprovante de pagamento.

**Fluxos Alternativos**
- A1 — Valor inferior ao total: O sistema bloqueia o registro e informa que pagamentos parciais não são permitidos.
- A2 — Aluno não encontrado: O sistema exibe mensagem de erro.

**RF Relacionados**
- RF03 — Controle de Pagamentos
- RF04 — Regularidade do Aluno

**RNF Relacionados**
- RNF02 — Segurança
- RNF03 — Performance

**RN Relacionadas**
- RN04 — Pagamento parcial
- RN07 — Atualização automática da regularidade

---

## UC05 — Validar Acesso pela Catraca

**Ator Principal**
Sistema de Catraca (API externa)

**Objetivo**
Validar automaticamente a entrada do aluno na academia via RFID.

**Pré-condições**
- Aluno deve possuir cartão RFID vinculado ao seu cadastro.
- Sistema de catraca deve estar integrado ao sistema FitPass.

**Pós-condições**
- Acesso liberado ou negado, com registro do evento no histórico.

**Fluxo Principal**
1. O aluno aproxima o cartão RFID da catraca.
2. A catraca envia o código RFID ao sistema via API REST.
3. O sistema verifica se o aluno está cadastrado e com situação regular.
4. O sistema retorna autorização de acesso.
5. A catraca libera a entrada e registra o acesso.

**Fluxos Alternativos**
- A1 — Aluno inadimplente: O sistema retorna negação de acesso e a catraca permanece bloqueada.
- A2 — RFID não reconhecido: O sistema retorna erro e a catraca permanece bloqueada.
- A3 — Falha de comunicação com a API: A catraca exibe erro de conexão.

**RF Relacionados**
- RF04 — Regularidade do Aluno
- RF05 — Controle de Acesso

**RNF Relacionados**
- RNF03 — Performance
- RNF06 — Integração

**RN Relacionadas**
- RN01 — Bloqueio por inadimplência

---

## UC06 — Agendar Aula

**Ator Principal**
Aluno

**Objetivo**
Permitir que o aluno visualize os horários disponíveis e reserve uma vaga em uma aula.

**Pré-condições**
- Aluno deve estar autenticado e com situação regular.
- Deve haver vagas disponíveis na aula desejada.

**Pós-condições**
- Reserva confirmada e notificação enviada ao aluno.

**Fluxo Principal**
1. O aluno acessa o módulo de agendamento de aulas.
2. O aluno visualiza os horários e modalidades disponíveis.
3. O aluno seleciona a aula desejada.
4. O sistema verifica a disponibilidade de vagas.
5. O sistema confirma a reserva.
6. O sistema envia notificação de confirmação ao aluno.

**Fluxos Alternativos**
- A1 — Aula sem vagas: O sistema exibe mensagem informando que a aula está lotada e bloqueia o agendamento.
- A2 — Aluno inadimplente: O sistema exibe mensagem e impede o agendamento.

**RF Relacionados**
- RF06 — Agendamento de Aulas
- RF10 — Notificações

**RNF Relacionados**
- RNF04 — Usabilidade
- RNF03 — Performance

**RN Relacionadas**
- RN01 — Bloqueio por inadimplência
- RN02 — Limite de vagas

---

## UC07 — Cancelar Agendamento de Aula

**Ator Principal**
Aluno

**Objetivo**
Permitir que o aluno cancele uma reserva de aula previamente realizada.

**Pré-condições**
- Aluno deve estar autenticado.
- Aluno deve possuir uma reserva ativa para a aula.
- O cancelamento deve ocorrer com pelo menos 1 hora de antecedência.

**Pós-condições**
- Reserva cancelada e vaga liberada para outros alunos.

**Fluxo Principal**
1. O aluno acessa o módulo de agendamentos.
2. O aluno localiza a reserva que deseja cancelar.
3. O aluno solicita o cancelamento.
4. O sistema verifica se o cancelamento está dentro do prazo permitido.
5. O sistema cancela a reserva e libera a vaga.
6. O sistema confirma o cancelamento ao aluno.

**Fluxos Alternativos**
- A1 — Cancelamento fora do prazo: O sistema exibe mensagem informando que o prazo de cancelamento foi encerrado.

**RF Relacionados**
- RF06 — Agendamento de Aulas

**RNF Relacionados**
- RNF04 — Usabilidade

**RN Relacionadas**
- RN03 — Cancelamento de agendamento

---

## UC08 — Registrar Presença em Aula

**Ator Principal**
Instrutor

**Objetivo**
Registrar a presença dos alunos em uma aula ministrada.

**Pré-condições**
- Instrutor deve estar autenticado.
- A aula deve estar cadastrada e em andamento.

**Pós-condições**
- Presença dos alunos registrada com sucesso no sistema.

**Fluxo Principal**
1. O instrutor acessa o módulo de lista de presença.
2. O instrutor seleciona a aula correspondente.
3. O sistema exibe a lista de alunos agendados para a aula.
4. O instrutor marca a presença dos alunos presentes.
5. O sistema salva o registro de presença.

**Fluxos Alternativos**
- A1 — Aluno presente mas sem agendamento: O instrutor pode incluir o aluno manualmente na lista.
- A2 — Aula não encontrada: O sistema exibe mensagem de erro.

**RF Relacionados**
- RF07 — Lista de Presença

**RNF Relacionados**
- RNF04 — Usabilidade
- RNF03 — Performance

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC09 — Realizar Avaliação Física

**Ator Principal**
Instrutor

**Objetivo**
Registrar a avaliação física de um aluno, incluindo dados como peso, IMC e percentual de gordura.

**Pré-condições**
- Instrutor deve estar autenticado.
- Aluno deve estar ativo e com situação regular.

**Pós-condições**
- Avaliação física registrada no histórico do aluno.

**Fluxo Principal**
1. O instrutor acessa o módulo de avaliações físicas.
2. O instrutor localiza o aluno pelo nome ou CPF.
3. O sistema verifica se o aluno está ativo e regular.
4. O instrutor preenche os dados da avaliação (peso, altura, IMC, percentual de gordura etc.).
5. O instrutor pode anexar arquivos complementares.
6. O sistema salva a avaliação no histórico do aluno.

**Fluxos Alternativos**
- A1 — Aluno inadimplente: O sistema exibe mensagem e impede o registro da avaliação.
- A2 — Dados incompletos: O sistema exibe mensagem indicando os campos obrigatórios.

**RF Relacionados**
- RF08 — Avaliação Física

**RNF Relacionados**
- RNF02 — Segurança
- RNF04 — Usabilidade

**RN Relacionadas**
- RN05 — Avaliação física
- RN06 — Acesso restrito por perfil

---

## UC10 — Emitir Relatório de Inadimplência

**Ator Principal**
Gerente

**Objetivo**
Gerar relatório com todos os alunos com mensalidade em atraso.

**Pré-condições**
- Gerente deve estar autenticado no sistema.

**Pós-condições**
- Relatório de inadimplência gerado e disponível para visualização ou exportação.

**Fluxo Principal**
1. O gerente acessa o módulo de relatórios.
2. O gerente seleciona o relatório de inadimplência.
3. O gerente define os filtros desejados (período, unidade etc.).
4. O sistema processa os dados e gera o relatório.
5. O gerente visualiza ou exporta o relatório.

**Fluxos Alternativos**
- A1 — Nenhum aluno inadimplente no período: O sistema exibe mensagem informando que não há registros.

**RF Relacionados**
- RF09 — Relatórios Gerenciais

**RNF Relacionados**
- RNF03 — Performance
- RNF05 — Escalabilidade

**RN Relacionadas**
- RN01 — Bloqueio por inadimplência
- RN06 — Acesso restrito por perfil

---

## UC11 — Emitir Relatório de Alunos Ativos

**Ator Principal**
Gerente

**Objetivo**
Gerar relatório com todos os alunos ativos na academia.

**Pré-condições**
- Gerente deve estar autenticado no sistema.

**Pós-condições**
- Relatório de alunos ativos gerado e disponível para visualização ou exportação.

**Fluxo Principal**
1. O gerente acessa o módulo de relatórios.
2. O gerente seleciona o relatório de alunos ativos.
3. O gerente aplica os filtros desejados (plano, modalidade, período).
4. O sistema processa os dados e gera o relatório.
5. O gerente visualiza ou exporta o relatório.

**Fluxos Alternativos**
- A1 — Nenhum aluno ativo encontrado: O sistema exibe mensagem informando ausência de registros.

**RF Relacionados**
- RF09 — Relatórios Gerenciais

**RNF Relacionados**
- RNF03 — Performance
- RNF05 — Escalabilidade

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC12 — Emitir Relatório de Histórico de Acessos

**Ator Principal**
Gerente

**Objetivo**
Gerar relatório com o histórico de entradas e saídas dos alunos pela catraca.

**Pré-condições**
- Gerente deve estar autenticado no sistema.

**Pós-condições**
- Relatório de acessos gerado e disponível para visualização ou exportação.

**Fluxo Principal**
1. O gerente acessa o módulo de relatórios.
2. O gerente seleciona o relatório de histórico de acessos.
3. O gerente define os filtros desejados (período, aluno, unidade).
4. O sistema processa os dados e gera o relatório.
5. O gerente visualiza ou exporta o relatório.

**Fluxos Alternativos**
- A1 — Nenhum acesso encontrado no período: O sistema exibe mensagem informando ausência de registros.

**RF Relacionados**
- RF05 — Controle de Acesso
- RF09 — Relatórios Gerenciais

**RNF Relacionados**
- RNF03 — Performance
- RNF05 — Escalabilidade

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC13 — Emitir Relatório de Ocupação de Aulas

**Ator Principal**
Gerente

**Objetivo**
Gerar relatório com a taxa de ocupação das aulas oferecidas pela academia.

**Pré-condições**
- Gerente deve estar autenticado no sistema.

**Pós-condições**
- Relatório de ocupação gerado e disponível para visualização ou exportação.

**Fluxo Principal**
1. O gerente acessa o módulo de relatórios.
2. O gerente seleciona o relatório de ocupação de aulas.
3. O gerente define os filtros desejados (período, modalidade, instrutor).
4. O sistema processa os dados e gera o relatório.
5. O gerente visualiza ou exporta o relatório.

**Fluxos Alternativos**
- A1 — Nenhuma aula registrada no período: O sistema exibe mensagem informando ausência de registros.

**RF Relacionados**
- RF09 — Relatórios Gerenciais

**RNF Relacionados**
- RNF03 — Performance
- RNF05 — Escalabilidade

**RN Relacionadas**
- RN02 — Limite de vagas
- RN06 — Acesso restrito por perfil

---

## UC14 — Enviar Notificação de Vencimento de Mensalidade

**Ator Principal**
Sistema

**Objetivo**
Notificar automaticamente o aluno sobre o vencimento próximo da mensalidade.

**Pré-condições**
- Aluno deve estar cadastrado e com e-mail ou contato registrado.
- Data de vencimento deve estar próxima (conforme regra configurada).

**Pós-condições**
- Notificação enviada ao aluno com sucesso.

**Fluxo Principal**
1. O sistema verifica diariamente as datas de vencimento das mensalidades.
2. O sistema identifica os alunos com vencimento próximo.
3. O sistema gera e envia a notificação ao aluno (e-mail ou app).
4. O sistema registra o envio da notificação.

**Fluxos Alternativos**
- A1 — Falha no envio: O sistema registra a falha e tenta reenviar posteriormente.

**RF Relacionados**
- RF10 — Notificações

**RNF Relacionados**
- RNF01 — Disponibilidade
- RNF03 — Performance

**RN Relacionadas**
- RN01 — Bloqueio por inadimplência
- RN07 — Atualização automática da regularidade

---

## UC15 — Enviar Notificação de Confirmação de Agendamento

**Ator Principal**
Sistema

**Objetivo**
Notificar o aluno automaticamente após a confirmação de um agendamento de aula.

**Pré-condições**
- Aluno deve ter realizado um agendamento com sucesso.
- Aluno deve possuir contato registrado (e-mail ou app).

**Pós-condições**
- Notificação de confirmação enviada ao aluno.

**Fluxo Principal**
1. O aluno confirma o agendamento de uma aula.
2. O sistema gera a notificação de confirmação.
3. O sistema envia a notificação ao aluno.
4. O sistema registra o envio.

**Fluxos Alternativos**
- A1 — Falha no envio: O sistema registra a falha e tenta reenviar posteriormente.

**RF Relacionados**
- RF06 — Agendamento de Aulas
- RF10 — Notificações

**RNF Relacionados**
- RNF01 — Disponibilidade
- RNF03 — Performance

**RN Relacionadas**
- RN02 — Limite de vagas

---

## UC16 — Enviar Notificação de Nova Avaliação Física Disponível

**Ator Principal**
Sistema

**Objetivo**
Notificar o aluno quando uma nova avaliação física estiver disponível para agendamento.

**Pré-condições**
- Aluno deve estar ativo e regular.
- Período mínimo entre avaliações deve ter sido cumprido.

**Pós-condições**
- Notificação enviada ao aluno informando a disponibilidade de nova avaliação.

**Fluxo Principal**
1. O sistema verifica periodicamente os históricos de avaliações dos alunos.
2. O sistema identifica os alunos aptos a realizar nova avaliação.
3. O sistema envia notificação ao aluno.
4. O sistema registra o envio.

**Fluxos Alternativos**
- A1 — Falha no envio: O sistema registra a falha e tenta reenviar posteriormente.
- A2 — Aluno inadimplente: O sistema não envia a notificação até a regularização.

**RF Relacionados**
- RF08 — Avaliação Física
- RF10 — Notificações

**RNF Relacionados**
- RNF01 — Disponibilidade

**RN Relacionadas**
- RN05 — Avaliação física

---

## UC17 — Consultar Histórico de Avaliações Físicas

**Ator Principal**
Aluno / Instrutor

**Objetivo**
Permitir a consulta ao histórico de avaliações físicas de um aluno.

**Pré-condições**
- Usuário deve estar autenticado.
- Aluno deve possuir ao menos uma avaliação registrada.

**Pós-condições**
- Histórico de avaliações exibido com sucesso.

**Fluxo Principal**
1. O usuário acessa o módulo de avaliações físicas.
2. O usuário localiza o aluno (se instrutor) ou acessa diretamente o próprio histórico (se aluno).
3. O sistema exibe a lista de avaliações registradas com datas e valores.
4. O usuário pode selecionar uma avaliação para ver os detalhes completos.

**Fluxos Alternativos**
- A1 — Nenhuma avaliação registrada: O sistema exibe mensagem informando ausência de histórico.

**RF Relacionados**
- RF08 — Avaliação Física

**RNF Relacionados**
- RNF02 — Segurança
- RNF04 — Usabilidade

**RN Relacionadas**
- RN05 — Avaliação física
- RN06 — Acesso restrito por perfil

---

## UC18 — Editar Dados Cadastrais do Aluno

**Ator Principal**
Recepcionista

**Objetivo**
Permitir a atualização dos dados pessoais, de contato ou de endereço de um aluno já cadastrado.

**Pré-condições**
- Recepcionista deve estar autenticada.
- Aluno deve estar cadastrado no sistema.

**Pós-condições**
- Dados do aluno atualizados com sucesso.

**Fluxo Principal**
1. A recepcionista acessa o módulo de cadastro de alunos.
2. A recepcionista localiza o aluno pelo nome ou CPF.
3. A recepcionista edita os campos desejados.
4. O sistema valida os dados alterados.
5. O sistema salva as alterações e confirma a atualização.

**Fluxos Alternativos**
- A1 — Dados inválidos: O sistema exibe mensagem de erro e solicita correção.
- A2 — Aluno não encontrado: O sistema exibe mensagem de erro.

**RF Relacionados**
- RF01 — Cadastro de Alunos

**RNF Relacionados**
- RNF02 — Segurança
- RNF04 — Usabilidade

**RN Relacionadas**
- RN06 — Acesso restrito por perfil

---

## UC19 — Gerar Boleto ou Link de Pagamento Online

**Ator Principal**
Sistema / Recepcionista

**Objetivo**
Gerar boleto bancário ou link de pagamento online para que o aluno quite sua mensalidade remotamente.

**Pré-condições**
- Aluno deve estar cadastrado no sistema.
- Mensalidade deve estar em aberto.

**Pós-condições**
- Boleto ou link de pagamento gerado e disponibilizado ao aluno.

**Fluxo Principal**
1. A recepcionista ou o sistema acessa o módulo de pagamentos.
2. Seleciona o aluno com mensalidade em aberto.
3. Seleciona a opção de gerar boleto ou link de pagamento online.
4. O sistema gera o documento de cobrança.
5. O sistema envia o boleto ou link ao e-mail do aluno.

**Fluxos Alternativos**
- A1 — Falha na geração do boleto: O sistema exibe mensagem de erro e registra a ocorrência.
- A2 — E-mail do aluno não cadastrado: O sistema exibe aviso e disponibiliza o boleto apenas para impressão.

**RF Relacionados**
- RF03 — Controle de Pagamentos

**RNF Relacionados**
- RNF02 — Segurança
- RNF01 — Disponibilidade

**RN Relacionadas**
- RN04 — Pagamento parcial
- RN07 — Atualização automática da regularidade

---

## UC20 — Consultar Regularidade do Aluno

**Ator Principal**
Recepcionista / Sistema de Catraca

**Objetivo**
Verificar se um aluno está com a mensalidade em dia e apto a utilizar os serviços da academia.

**Pré-condições**
- Aluno deve estar cadastrado no sistema.

**Pós-condições**
- Situação de regularidade do aluno exibida ou retornada ao sistema solicitante.

**Fluxo Principal**
1. A recepcionista ou o sistema de catraca solicita a verificação da regularidade de um aluno.
2. O sistema busca os dados de pagamento do aluno.
3. O sistema verifica se há mensalidade em atraso há mais de 5 dias.
4. O sistema retorna o status: regular ou inadimplente.
5. A recepcionista ou catraca executa a ação correspondente (liberar ou bloquear acesso).

**Fluxos Alternativos**
- A1 — Aluno inadimplente: O sistema retorna status de bloqueio e exibe data do último pagamento.
- A2 — Aluno não encontrado: O sistema retorna mensagem de erro.

**RF Relacionados**
- RF04 — Regularidade do Aluno
- RF05 — Controle de Acesso

**RNF Relacionados**
- RNF03 — Performance
- RNF06 — Integração

**RN Relacionadas**
- RN01 — Bloqueio por inadimplência
- RN07 — Atualização automática da regularidade
