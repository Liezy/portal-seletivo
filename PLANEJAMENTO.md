# Planejamento — Portal de Processos Seletivos

## Objetivo e escopo

Desenvolver incrementalmente um portal de processos seletivos um curso. O primeiro curso será a **Especialização em Gestão de Incêndios Florestais**.

Stack: **Django, Django Templates, Tailwind CSS com daisyUI e SQLite** inicialmente. Manter o uso do ORM e das migrações do Django para permitir futura migração para **PostgreSQL**.

Cada item deve ser implementado individualmente, verificado e aprovado pelo usuário antes do avanço. As regras acadêmicas e administrativas dependerão do edital e de confirmação do usuário.

## Preparação

- [x] Criar este planejamento com sete etapas e tarefas verificáveis.
- [x] Criar `AGENTS.md` com as instruções de trabalho.
- [x] Preparar o Git local na branch `main`, ignorar dados locais e remover a chave fixa do Django antes do versionamento.
- [x] Conectar ao repositório informado pelo usuário no GitHub e verificar o envio inicial.

Verificação: conferir a existência dos dois arquivos, as sete etapas e as regras solicitadas. Nenhuma implementação da aplicação foi realizada nesta preparação. A pasta já continha `config/`, `venv/`, `manage.py` e `db.sqlite3`; esses itens não foram alterados ou validados nesta tarefa.

## 1. Estrutura inicial

- [x] Inspecionar a estrutura Django existente e registrar o que pode ser aproveitado. Verificar: inventário de configuração, aplicações e dependências.
- [x] Identificar e registrar as versões instaladas de Python, Django e dependências. Verificar: versões obtidas do ambiente virtual e registradas no inventário.
- [x] Definir as dependências mínimas em arquivo e verificar uma instalação reproduzível em ambiente virtual limpo.
- [x] Organizar as aplicações e configurações mínimas do projeto. Verificar: `python manage.py check` sem erros.
- [x] Configurar SQLite e executar as migrações iniciais. Verificar: configuração existente confirmada e 18 migrações nativas já aplicadas, conforme inspeção.
- [x] Configurar Django Templates, arquivos estáticos e Tailwind CSS. Verificar: página de desenvolvimento com um estilo Tailwind carregado.
- [x] Integrar daisyUI ao Tailwind CSS. Verificar: componente daisyUI renderizado com os estilos compilados e servidos pelo Django.
- [x] Definir o tema visual do portal com daisyUI. Verificar: tema claro com cores semânticas consistentes, botão daisyUI e foco visível; campos serão conferidos quando seus formulários forem criados.
- [x] Criar o template base com idioma português e estrutura responsiva. Verificar: renderização em telas pequenas e grandes.
- [x] Documentar a instalação e a execução local. Verificar: seguir os passos em um ambiente limpo.

### Conclusão da etapa 1

Autorização do usuário: concluir todas as tarefas restantes desta etapa, sem pausas entre elas.

- Dependências Python fixadas em `requirements.txt` e instaladas no ambiente separado `.venv-verificacao/`; `pip check` sem incompatibilidades.
- Tailwind CSS e CLI 4.3.4 e daisyUI 5.7.50 fixados, com `package-lock.json`; `npm ci` e `npm run build:css` executados com sucesso. A consulta npm informou zero vulnerabilidades.
- Aplicação `core` criada para a rota inicial, usando `TemplateView` nativa; sem modelos ou regras de seleção.
- Django Templates, arquivos estáticos, idioma `pt-br` e fuso `America/Sao_Paulo` configurados. Tema claro inicial com verde, azul e foco visível; sem alegação de identidade visual oficial.
- Template base com cabeçalho, rodapé, link para pular ao conteúdo e blocos reutilizáveis. Página mínima informa que o portal está em preparação.
- `README.md` documenta instalação, compilação, execução, configuração de chave, estrutura e verificações. Não há carregamento automático de `.env`.
- Verificações: `manage.py check`, `makemigrations --check --dry-run`, `migrate --check`, coleta de estáticos simulada, migrações em SQLite temporário vazio e `git diff --check` sem erros. Página e CSS retornaram HTTP 200; redirecionamento do Admin, idioma, fuso e localização do CSS conferidos.
- Renderização inspecionada no Edge headless em 500 × 900 e 1440 × 1000. A janela de 390 px ficou limitada pela largura mínima do navegador; não foi considerada uma validação de viewport móvel de 390 px. Navegação real por teclado e formulários ficam para a revisão de acessibilidade; foco e link de salto estão implementados.

Etapa 1 concluída. Etapa 2 depende de nova aprovação. Alterações reunidas em commit local por solicitação do usuário; envio ao GitHub pendente.

### Inventário da estrutura existente — 05/11/2026

- **Base reutilizável:** `manage.py` e pacote `config/` com configurações, rotas e pontos de entrada ASGI e WSGI. Não é necessário recriar o projeto.
- **Ambiente observado:** `venv/` com Python 3.14.7, Django 6.1.3, asgiref 3.13.0, sqlparse 0.6.1, tzdata 2026.6 e pip 26.2.1. Versões obtidas diretamente do ambiente local; a definição das dependências e a instalação reproduzível ficam para a próxima tarefa.
- **Aplicações:** somente as nativas `admin`, `auth`, `contenttypes`, `sessions`, `messages` e `staticfiles`. Nenhuma aplicação de domínio criada.
- **Banco:** SQLite configurado em `db.sqlite3`; todas as 18 migrações nativas listadas estão aplicadas. O banco pode ser aproveitado no desenvolvimento e permanece fora do Git. Nenhum dado de usuário foi consultado.
- **Rotas:** somente `admin/`; ainda não há página pública.
- **Templates e estilos:** backend Django Templates com `APP_DIRS=True` e `DIRS=[]`; `STATIC_URL='static/'`. Ainda não há templates próprios, configuração de compilação Tailwind ou daisyUI.
- **Configurações observadas:** `DEBUG=True`, `ALLOWED_HOSTS=[]`, idioma `en-us`, fuso `UTC` e backend de e-mail em console. Localização para português e fuso do projeto ficam para a tarefa de configurações mínimas.
- **Chave do Django:** leitura de `DJANGO_SECRET_KEY` do ambiente com geração temporária como alternativa; sem chave fixa versionada. A alternativa temporária não preserva sessões entre reinícios.
- **Versionamento:** branch `main` acompanha `origin/main`; `.gitignore` já protege ambiente virtual, SQLite, arquivos `.env` e documentos enviados. Alterações locais anteriores em `AGENTS.md` e neste planejamento foram preservadas.
- **Pendências de estrutura:** arquivo de dependências, documentação de instalação, aplicações do portal, templates, estilos e configuração de produção ainda não preparados.

Verificações executadas: inventário dos arquivos e configurações, `python --version`, `python -m pip list`, `python manage.py check` (sem problemas) e `python manage.py showmigrations` (18 migrações aplicadas), usando `venv/Scripts/python.exe`. Nenhuma dependência instalada e nenhuma configuração da aplicação alterada nesta tarefa.

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

Uso de daisyUI registrado no planejamento e em `AGENTS.md`; integração local concluída na etapa 1.

| Tarefa | Situação | Verificação | Próximo passo |
| --- | --- | --- | --- |
| Preparação do planejamento e das instruções | Concluída | Arquivos conferidos, sete etapas e regras presentes | Aguardar aprovação do usuário para iniciar a primeira tarefa da etapa 1 |
| Setup Git local | Concluída | Branch `main` criada; exclusões conferidas com `git check-ignore`; `manage.py check` sem erros; chave fixa removida | Conexão com GitHub concluída |
| Conexão com GitHub | Concluída | Remoto `origin`: `git@github.com:Liezy/portal-seletivo.git`; autenticação SSH e envio inicial bem-sucedidos; `main` acompanha `origin/main` | Aguardar aprovação do usuário para iniciar a primeira tarefa da etapa 1 |
| Etapa 1 — Inspeção da estrutura existente | Concluída | Inventário registrado; `manage.py check` sem problemas; 18 migrações nativas aplicadas | Aguardar aprovação para definir e registrar versões e dependências mínimas com instalação reproduzível |
| Revisão dos checks da etapa 1 | Concluída | Inspeção, versões instaladas e SQLite com migrações marcados; instalação reproduzível separada como pendência | Aguardar aprovação para preparar o arquivo de dependências e validar a instalação limpa |
| Etapa 1 — Estrutura inicial completa | Concluída | Instalações Python e npm reproduzidas; CSS compilado; verificações Django, banco vazio, HTTP e inspeção visual realizadas; README criado | Aguardar aprovação para iniciar a etapa 2 |
