# Documentação Técnica - Sistema de Biblioteca CLI

Esta documentação é destinada a desenvolvedores e engenheiros de software que darão manutenção ou integrarão novos módulos a este sistema. O sistema utiliza uma arquitetura monolítica procedimental simples baseada em terminal (CLI), com persistência de dados local em arquivos planos (`.txt`).

## 1. Estrutura do Banco de Dados Relacional Primitivo

O sistema utiliza delimitadores de ponto e vírgula (`;`) para separar as colunas em arquivos de texto.

### Livros (`d.txt`)
* **Índice [0] (ID):** Identificador único do livro (string numérica).
* **Índice [1] (Título):** Nome da obra literária.
* **Índice [2] (Autor):** Autor da obra.
* **Índice [3] (Status):** Flag binária de disponibilidade (`1` para Disponível, `0` para Emprestado/Indisponível).

### Usuários (`u.txt`)
* **Índice [0] (ID):** Identificador único do usuário (string numérica).
* **Índice [1] (Nome):** Nome do usuário.
* **Índice [2] (Status de Pendência):** Flag binária de restrição (`1` se o usuário já possui um livro emprestado, `0` se está livre).

---

## 2. Referência da API Interna (Funções)

### `m1() -> None`
* **Descrição:** Executa o *bootstrap* (inicialização) do sistema. Verifica se os arquivos físicos de dados (`d.txt` e `u.txt`) existem no diretório de execução. Se não existirem, cria-os e injeta dados iniciais (*seed*).

### `m2() -> list[list[str]]`
* **Descrição:** Camada de leitura de dados (*Data Fetcher*). Abre o arquivo `d.txt`, remove quebras de linha (`\n`), ignora linhas vazias e quebra as strings por `;`, retornando uma matriz bidimensional (lista de listas).

### `m3(xyz: list[list[str]]) -> None`
* **Descrição:** Camada de persistência de dados (*Data Committer*). Recebe a matriz atualizada do acervo de livros via argumento `xyz`, reconverte a estrutura unindo os elementos por `;` e sobrescreve o arquivo `d.txt`.

### `f1() -> None`
* **Descrição:** Controlador de visualização (*View Controller*). Consome a matriz de dados da função `m2()` e imprime o acervo no terminal de forma legível, traduzindo o status binário `1` ou `0` para as strings "Disponivel" ou "Levaram".

### `f2