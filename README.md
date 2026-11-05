# Portal de Processos Seletivos

Portal para cursos de especialização da UFT, começando pela Especialização em Gestão de Incêndios Florestais.

## Ambiente

- Python 3.14 (verificado com 3.14.7) e Django 6.1.3.
- Node.js 22 ou superior (verificado com 24.21.0) e npm (verificado com 11.19.0).
- Django Templates, Tailwind CSS 4.3.4, daisyUI 5.7.50 e SQLite.

As dependências Python estão fixadas em `requirements.txt`. As ferramentas de CSS estão fixadas em `package.json` e `package-lock.json`. Node é necessário para compilar os estilos; a aplicação é executada pelo Django.

## Instalação local no Windows / PowerShell

Na raiz do repositório:

```powershell
py -3.14 -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
npm.cmd ci
npm.cmd run build:css
.\venv\Scripts\python.exe manage.py migrate
.\venv\Scripts\python.exe manage.py check
.\venv\Scripts\python.exe manage.py runserver
```

Acesse <http://127.0.0.1:8000/>. O uso direto do executável do ambiente dispensa ativação e mudanças na política de execução do PowerShell.

No Linux/macOS, crie o ambiente com `python3 -m venv venv`, use `venv/bin/python` no lugar de `.\venv\Scripts\python.exe` e `npm` no lugar de `npm.cmd`.

## Desenvolvimento dos estilos

Em outro terminal, mantenha a recompilação ativa enquanto edita os templates:

```powershell
npm.cmd run watch:css
```

O arquivo fonte é `assets/css/app.css`; o resultado é `static/css/app.css`, ignorado pelo Git. Execute o build após clonar e antes de abrir a página. As classes dos templates em `templates/` são incluídas na compilação. Se novos diretórios de templates forem criados dentro de aplicações, acrescente-os com `@source` no CSS fonte. Use nomes de classes completos nos templates, evitando montá-los por concatenação.

O tema inicial é claro, com verde como cor principal, azul como secundária e foco visível. É uma escolha inicial do projeto, sem equivalência declarada ao manual de marca da UFT. Componentes usam daisyUI; layout e responsividade usam utilitários Tailwind.

## Configuração local

SQLite usa `db.sqlite3`, ignorado pelo Git. As configurações locais usam português brasileiro, `America/Sao_Paulo` e e-mail no console. A estrutura mantém o ORM e as migrações para uma futura mudança para PostgreSQL.

Para manter sessões válidas entre reinícios, defina uma chave no terminal antes de iniciar o servidor:

```powershell
$env:DJANGO_SECRET_KEY = (.\venv\Scripts\python.exe -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())")
.\venv\Scripts\python.exe manage.py runserver
```

Sem essa variável, uma chave temporária é gerada a cada inicialização. Arquivos `.env` não são carregados automaticamente. Não versione chaves. O ambiente atual usa `DEBUG=True` e destina-se ao desenvolvimento; a configuração de produção será feita na etapa 7.

Para acessar `/admin/`, crie seu próprio administrador:

```powershell
.\venv\Scripts\python.exe manage.py createsuperuser
```

## Estrutura

- `config/`: configurações e rotas principais do Django.
- `core/`: rota inicial e configuração da aplicação base; sem modelos de negócio nesta etapa.
- `templates/base.html`: idioma, cabeçalho, rodapé, navegação por teclado e blocos reutilizáveis.
- `templates/core/home.html`: página mínima de apresentação e situação do portal.
- `assets/css/`: fontes de estilos e tema daisyUI.
- `static/css/`: CSS compilado servido pelo Django no desenvolvimento.
- `PLANEJAMENTO.md`: tarefas e registros de verificação.
- `AGENTS.md`: instruções de trabalho.

## Verificações

```powershell
.\venv\Scripts\python.exe -m pip check
.\venv\Scripts\python.exe manage.py check
.\venv\Scripts\python.exe manage.py makemigrations --check --dry-run
.\venv\Scripts\python.exe manage.py migrate --check
npm.cmd run build:css
git diff --check
```

Após compilar, confira a página em tela pequena e desktop e navegue com Tab para verificar foco e o link “Pular para o conteúdo”. Os processos, editais e inscrições serão implementados nas etapas seguintes.

Integração dos estilos baseada na documentação oficial do [Tailwind CLI](https://tailwindcss.com/docs/installation/tailwind-cli) e do [daisyUI](https://daisyui.com/docs/install/).
