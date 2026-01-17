# 📋 Gerenciador de Boards de Tarefas (Kanban)

Projeto desenvolvido durante o Bootcamp CI&T: Backend com Java & AWS. O sistema consiste em uma aplicação de console para gerenciamento de fluxos de trabalho, permitindo a criação de quadros, colunas e cartões, com controle de bloqueios e movimentações.

## 🚀 Funcionalidades

- **Gerenciamento de Boards:** Criar, listar, selecionar e excluir boards.
- **Configuração de Colunas:** Suporte a colunas padrão (Pendente, Fazendo, Feito) e colunas personalizadas.
- **Controle de Cards:** Criação de tarefas e movimentação entre colunas.
- **Sistema de Bloqueio:** Bloquear e desbloquear cards com registro de motivos (persistidos no banco de dados).
- **Persistência de Dados:** Integração total com MySQL e controle de versão de banco com Liquibase.

## 🛠️ Tecnologias Utilizadas

- **Java 17+**
- **MySQL 8.0**
- **JDBC** (Java Database Connectivity)
- **Liquibase** (Gerenciamento de migrações de banco de dados)
- **Maven** (Gerenciamento de dependências)

## 🏗️ Arquitetura do Projeto

O projeto foi estruturado seguindo boas práticas de arquitetura em camadas:
- `ui`: Interface de usuário via console.
- `service`: Camada de regras de negócio e validações.
- `persistence`: Camada de acesso a dados (DAO) e entidades.
- `dto`: Objetos de transferência de dados para comunicação entre camadas.
- `exception`: Tratamento de exceções personalizadas (ex: `CardBlockedException`, `CardFinishedException` e `EntityNotFoundException`).

## 🧠 Desafios e Soluções

Durante o desenvolvimento, surgiram desafios técnicos que exigiram soluções específicas:

1. **Gestão de Migrações (Liquibase):** - *Desafio:* Erros de Checksum ao alterar scripts de migração já executados.
    - *Solução:* Utilização do comando `clearCheckSums` e reset planejado do schema para garantir a integridade entre o código Java e a estrutura do MySQL.

2. **Integridade Referencial:** - *Desafio:* Garantir que, ao excluir um board, todos os itens dependentes (colunas e cards) fossem removidos.
    - *Solução:* Configuração de `ON DELETE CASCADE` nas chaves estrangeiras via scripts Liquibase.

3. **Case Sensitivity no Banco de Dados:**
    - *Desafio:* Conflitos de nomes de tabelas entre ambientes Windows e Linux (Docker).
    - *Solução:* Padronização de todos os identificadores de tabelas e colunas para letras minúsculas (`snake_case`).

4. **Sintaxe SQL e JDBC:**
    - *Desafio:* Erros de parâmetros não especificados em `PreparedStatements`.
    - *Solução:* Ajuste rigoroso no índice dos parâmetros e garantia de preenchimento de todos os `?` antes da execução das queries.

## 📝 Observações Finais

Este projeto foi fundamental para consolidar conhecimentos em **JDBC puro**, reforçando a importância de entender como a aplicação se comunica com o banco de dados antes de partir para frameworks de abstração como o Hibernate/JPA. A implementação do sistema de bloqueio de cards simula cenários reais de impedimentos em metodologias ágeis.

## Autor do projeto
Gabriel de Souza Conceição