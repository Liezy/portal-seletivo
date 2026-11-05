# Planejamento — Portal de Processos Seletivos da UFT

## Objetivo e escopo

Desenvolver incrementalmente um portal de processos seletivos para cursos de especialização da UFT. O primeiro curso será a **Especialização em Gestão de Incêndios Florestais**.

Stack: **Django, Django Templates, Tailwind CSS e SQLite** inicialmente. Manter o uso do ORM e das migrações do Django para permitir futura migração para **PostgreSQL**.

Cada item deve ser implementado individualmente, verificado e aprovado pelo usuário antes do avanço. As regras acadêmicas e administrativas dependerão do edital e de confirmação do usuário.

## Preparação

- [x] Criar este planejamento com sete etapas e tarefas verificáveis.
- [x] Criar `AGENTS.md` com as instruções de trabalho.
- [x] Preparar o Git local na branch `main`, ignorar dados locais e remover a chave fixa do Django antes do versionamento.
- [x] Conectar ao repositório informado pelo usuário no GitHub e verificar o envio inicial.

Verificação: conferir a existência dos dois arquivos, as sete etapas e as regras solicitadas. Nenhuma implementação da aplicação foi realizada nesta preparação. A pasta já continha `config/`, `venv/`, `manage.py` e `db.sqlite3`; esses itens não foram alterados ou validados nesta tarefa.

## 1. Estrutura inicial

- [ ] Inspecionar a estrutura Django existente e registrar o que pode ser aproveitado. Verificar: inventário de configuração, aplicações e dependências.
- [ ] Confirmar e registrar as versões de Python e Django e as dependências mínimas. Verificar: instalação reproduzível em ambiente virtual.
- [ ] Organizar as aplicações e configurações mínimas do projeto. Verificar: `python manage.py check` sem erros.
- [ ] Configurar SQLite e executar as migrações iniciais. Verificar: migrações aplicadas sem erros.
- [ ] Configurar Django Templates, arquivos estáticos e Tailwind CSS. Verificar: página de desenvolvimento com um estilo Tailwind carregado.
- [ ] Criar o template base com idioma português e estrutura responsiva. Verificar: renderização em telas pequenas e grandes.
- [ ] Documentar a instalação e a execução local. Verificar: seguir os passos em um ambiente limpo.

## 2. Portal público

- [ ] Definir os dados mínimos de cursos e processos seletivos. Verificar: campos e relações aprovados antes da implementação.
- [ ] Criar os modelos de curso e processo seletivo. Verificar: migrações aplicadas e relações válidas.
- [ ] Cadastrar os dados iniciais do curso de Gestão de Incêndios Florestais. Verificar: nome e informações conferidos com o usuário.
- [ ] Criar a página inicial com os processos publicados. Verificar: estados com lista preenchida e vazia.
- [ ] Criar a página de detalhes do processo seletivo. Verificar: curso, descrição, período e situação exibidos corretamente.
- [ ] Exibir edital e cronograma públicos. Verificar: links acessíveis e datas correspondentes ao cadastro.
- [ ] Restringir a exibição pública aos processos publicados. Verificar: processos não publicados inacessíveis por lista e endereço direto.

## 3. Administração

- [ ] Configurar o Django Admin para cursos e processos seletivos. Verificar: criação, edição e consulta por usuário autorizado.
- [ ] Configurar busca e filtros úteis no Admin. Verificar: localizar registros por curso, processo e situação.
- [ ] Permitir gerenciar editais e cronogramas pelo Admin. Verificar: alterações refletidas no portal público.
- [ ] Validar datas e campos obrigatórios do processo seletivo. Verificar: dados inconsistentes rejeitados com mensagens claras.
- [ ] Configurar grupos e permissões administrativas nativas. Verificar: usuário sem permissão não consegue consultar ou alterar recursos restritos.
- [ ] Controlar publicação e encerramento do processo. Verificar: mudança de situação refletida nas páginas públicas.

## 4. Autenticação e inscrição

- [ ] Confirmar os dados exigidos do candidato e as regras de inscrição. Verificar: lista de campos e regras aprovada.
- [ ] Implementar cadastro de candidato com validação de senha do Django. Verificar: cadastro válido aceito e dados inválidos rejeitados.
- [ ] Implementar entrada e saída com recursos nativos do Django. Verificar: acesso autenticado e encerramento de sessão.
- [ ] Implementar recuperação de senha. Verificar: fluxo completo com backend de e-mail de desenvolvimento.
- [ ] Criar o modelo de inscrição associado ao candidato e ao processo. Verificar: relações e restrições de duplicidade conforme regras aprovadas.
- [ ] Criar o formulário de inscrição. Verificar: dados válidos salvos e erros apresentados junto aos campos.
- [ ] Restringir inscrições ao período permitido. Verificar: antes, durante e depois do prazo, considerando o fuso configurado.
- [ ] Criar confirmação de envio com identificador da inscrição. Verificar: confirmação vinculada ao candidato correto.
- [ ] Restringir acesso aos dados da inscrição ao seu titular e aos administradores autorizados. Verificar: tentativa de acesso por outro candidato negada.

## 5. Documentos e acompanhamento

- [ ] Confirmar documentos exigidos, formatos, limites de tamanho e regras de substituição. Verificar: requisitos aprovados.
- [ ] Implementar envio e validação de documentos da inscrição. Verificar: arquivos permitidos aceitos e inválidos rejeitados.
- [ ] Proteger o acesso aos documentos enviados. Verificar: acesso anônimo e de outro candidato negado, inclusive por endereço direto.
- [ ] Permitir consultar e substituir documentos conforme o prazo e as regras aprovadas. Verificar: substituições permitidas e bloqueadas nos cenários previstos.
- [ ] Criar a área do candidato com suas inscrições e documentos. Verificar: exibição exclusiva dos dados do titular.
- [ ] Exibir a situação da inscrição e eventuais pendências. Verificar: informações consistentes com os registros administrativos.
- [ ] Registrar mudanças de situação com data e responsável. Verificar: histórico disponível para consulta autorizada.

## 6. Seleção e resultados

- [ ] Confirmar etapas de avaliação, critérios, notas, desempates e regras de recursos do edital. Verificar: regras aprovadas antes de codificar cálculos.
- [ ] Permitir análise e homologação das inscrições por usuários autorizados. Verificar: decisão, responsável e justificativa registrados.
- [ ] Implementar registro de avaliações conforme os critérios aprovados. Verificar: limites de notas e permissões respeitados.
- [ ] Implementar cálculo e classificação conforme o edital. Verificar: exemplos conferidos manualmente, incluindo empates.
- [ ] Implementar publicação de resultados preliminares. Verificar: somente dados e resultados autorizados ficam públicos.
- [ ] Implementar envio e análise de recursos, se previstos. Verificar: prazo, acesso do titular e registro da decisão.
- [ ] Implementar publicação do resultado final. Verificar: classificação coerente com decisões e avaliações finais.

## 7. Testes e publicação

- [ ] Revisar os testes dos fluxos de inscrição, prazos, permissões e seleção. Verificar: suíte executada sem falhas.
- [ ] Revisar formulários, navegação por teclado e responsividade. Verificar: fluxos principais utilizáveis em dispositivos móveis e desktop.
- [ ] Definir o ambiente de hospedagem e a necessidade de PostgreSQL. Verificar: decisão e requisitos de infraestrutura documentados.
- [ ] Se aprovada a migração para PostgreSQL, preparar e validar a transferência de dados. Verificar: migrações, contagens e relações preservadas em ambiente de teste.
- [ ] Configurar segredos, hosts permitidos, HTTPS e modo de produção. Verificar: revisão de `python manage.py check --deploy` no ambiente de destino.
- [ ] Configurar arquivos estáticos, documentos privados e envio de e-mails. Verificar: estilos, controle de acesso e recuperação de senha no ambiente de destino.
- [ ] Preparar backup e restauração do banco e dos documentos. Verificar: restauração testada em ambiente separado.
- [ ] Documentar publicação, manutenção e reversão de versão. Verificar: procedimentos executáveis e conferidos.
- [ ] Preparar uma versão para homologação do usuário. Verificar: fluxo completo de um processo seletivo com dados de teste.
- [ ] Publicar após aprovação explícita do usuário. Verificar: portal acessível e fluxos essenciais conferidos em produção.

## Registro de conclusões

| Tarefa | Situação | Verificação | Próximo passo |
| --- | --- | --- | --- |
| Preparação do planejamento e das instruções | Concluída | Arquivos conferidos, sete etapas e regras presentes | Aguardar aprovação do usuário para iniciar a primeira tarefa da etapa 1 |
| Setup Git local | Concluída | Branch `main` criada; exclusões conferidas com `git check-ignore`; `manage.py check` sem erros; chave fixa removida | Conexão com GitHub concluída |
| Conexão com GitHub | Concluída | Remoto `origin`: `git@github.com:Liezy/portal-seletivo.git`; autenticação SSH e envio inicial bem-sucedidos; `main` acompanha `origin/main` | Aguardar aprovação do usuário para iniciar a primeira tarefa da etapa 1 |
