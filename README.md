1. Requisitos
Objetivo do Sistema

Gerenciar o empréstimo e devolução de livros utilizando arquivos de texto para armazenamento dos dados.

Funcionalidades
Visualizar livros cadastrados.
Realizar empréstimos de livros.
Registrar devoluções.
Controlar disponibilidade dos livros.
Impedir que um usuário possua mais de um livro emprestado.
Regras de Negócio
Apenas livros disponíveis podem ser emprestados.
Um usuário pode possuir apenas um livro por vez.
Apenas livros emprestados podem ser devolvidos.
2. Design da Arquitetura
Camada de Dados

Responsável pelo armazenamento em arquivos.

Arquivos:

d.txt → Livros
u.txt → Usuários
Camada de Regras de Negócio

Responsável pelas validações.

Funções:

f2() → Empréstimo
f3() → Devolução
Camada de Interface

Responsável pela interação com o usuário.

Funções:

main()
listaCoisas()
3. Fluxo de Dados
Usuário
 ↓
Menu Principal
 ↓
Escolha da Operação
 ↓
Validação das Regras
 ↓
Leitura/Escrita dos Arquivos
 ↓
Resultado ao Usuário