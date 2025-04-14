# Meu Blog Pessoal

Este é o repositório do meu blog pessoal, construído com [Hugo](https://gohugo.io/) e o tema [Stack](https://github.com/CaiJimmy/hugo-theme-stack/).

## Pré-requisitos

- [Hugo](https://gohugo.io/) (versão extended)
- Git

## Instalação

### 1. Instalar Hugo

#### macOS (usando Homebrew):
```bash
brew install hugo
```

#### Windows (usando Chocolatey):
```bash
choco install hugo-extended
```

#### Linux:
```bash
snap install hugo
```

### 2. Clonar o repositório
```bash
git clone --recursive https://github.com/seu-usuario/seu-blog.git
cd seu-blog
```

O flag `--recursive` é importante para clonar também o submódulo do tema.

### 3. Atualizar submódulos (caso necessário)
```bash
git submodule update --init --recursive
```

## Executando localmente

Para iniciar o servidor de desenvolvimento:

```bash
hugo server -D
```

O site estará disponível em `http://localhost:1313/`

## Criando novo conteúdo

Para criar um novo post:

```bash
hugo new content posts/nome-do-post.md
```

## Estrutura do projeto

- `content/`: Contém todo o conteúdo do site
  - `posts/`: Artigos do blog
  - `about.md`: Página Sobre
- `themes/stack/`: Tema Stack
- `hugo.toml`: Arquivo de configuração do Hugo

## Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes. 