# 📅 Agendador de Horários — API REST

API REST desenvolvida em **Java com Spring Boot** para gerenciamento de agendamentos de horários.

O projeto implementa operações de **CRUD (Create, Read, Update e Delete)** e possui uma regra de negócio para evitar a duplicidade de horários para o mesmo serviço.

O objetivo principal é aplicar conceitos de desenvolvimento de APIs REST, organização em camadas, persistência com JPA e integração com banco de dados.

## 🚀 Funcionalidades

* Criar um novo agendamento;
* Consultar agendamentos de um determinado dia;
* Alterar um agendamento existente;
* Excluir um agendamento;
* Validar disponibilidade de horário;
* Impedir conflitos de horário para o mesmo serviço;
* Persistir os dados utilizando JPA;
* Utilizar banco H2 em memória para desenvolvimento e testes.

## 🛠️ Tecnologias

* **Java 21**
* **Spring Boot**
* **Spring Web**
* **Spring Data JPA**
* **Hibernate**
* **H2 Database**
* **Lombok**
* **Maven**

As dependências e a versão do Java estão definidas no `pom.xml` do projeto.

## 🏗️ Estrutura do projeto

A aplicação utiliza uma organização simples em camadas:

```text
src/main/java
├── controller
│   └── AgendamentoController.java
│
├── services
│   └── AgendamentoService.java
│
└── infrastructure
    ├── entity
    │   └── Agendamento.java
    │
    └── repository
        └── AgendamentoRepository.java
```

### Controller

O `AgendamentoController` é responsável por receber as requisições HTTP e disponibilizar os endpoints da API.

Ele possui operações para **POST, GET, PUT e DELETE** de agendamentos.

### Service

O `AgendamentoService` concentra as principais regras de negócio da aplicação.

Entre elas está a verificação de disponibilidade do horário antes de realizar um novo agendamento. Caso o horário esteja ocupado, a aplicação retorna uma exceção informando que o horário já está preenchido.

### Entity

A entidade `Agendamento` representa os dados armazenados no banco.

Atualmente possui informações como:

* ID;
* Serviço;
* Profissional;
* Data e horário do agendamento;
* Cliente;
* Telefone do cliente;
* Data de inserção.

A entidade utiliza JPA para realizar o mapeamento objeto-relacional.

### Repository

O `AgendamentoRepository` utiliza `JpaRepository` para facilitar a comunicação com o banco de dados.

Também possui consultas específicas para:

* Verificar conflitos de horário;
* Buscar agendamentos por período;
* Localizar um agendamento por data, horário e cliente;
* Excluir um agendamento por data, horário e cliente.

## 🔌 Endpoints

A API utiliza o recurso `/agendamentos`.

| Método   | Endpoint                                                         | Função                        |
| -------- | ---------------------------------------------------------------- | ----------------------------- |
| `POST`   | `/agendamentos`                                                  | Criar agendamento             |
| `GET`    | `/agendamentos?data={data}`                                      | Buscar agendamentos de um dia |
| `PUT`    | `/agendamentos?cliente={cliente}&dataHoraAgendamento={dataHora}` | Alterar agendamento           |
| `DELETE` | `/agendamentos?cliente={cliente}&dataHoraAgendamento={dataHora}` | Excluir agendamento           |

Os endpoints acima correspondem às operações implementadas no `AgendamentoController`.

## 🗄️ Banco de dados

Durante o desenvolvimento, o projeto utiliza o **H2 Database em memória**.

A configuração está localizada em:

```text
src/main/resources/application.properties
```

A aplicação utiliza:

```text
jdbc:h2:mem:agendamentos-db
```

Também está habilitado o **H2 Console**, disponível em:

```text
/h2-console
```

## ▶️ Como executar

### Pré-requisitos

* Java 21;
* Maven;
* IDE de sua preferência.

### Executando o projeto

Clone o repositório:

```bash
git clone https://github.com/vitorio-santos/Projeto-CRUD-Java.git
```

Entre na pasta da aplicação:

```bash
cd Projeto-CRUD-Java/agendador-horario
```

Execute o projeto com o Maven:

```bash
./mvnw spring-boot:run
```

No Windows:

```bash
mvnw.cmd spring-boot:run
```

Após a inicialização, a API poderá ser acessada localmente pela porta padrão do Spring Boot.

## 📌 Exemplo de agendamento

Exemplo de requisição para criação:

```json
{
  "servico": "Corte de cabelo",
  "profissional": "João",
  "dataHoraAgendamento": "2026-08-10T14:00:00",
  "cliente": "Maria",
  "telefoneCliente": "81999999999"
}
```

## 🎯 Objetivo do projeto

Este projeto foi desenvolvido como prática de conceitos fundamentais de desenvolvimento backend com Java, incluindo:

* Desenvolvimento de API REST;
* Operações CRUD;
* Spring Boot;
* Injeção de dependências;
* Arquitetura em camadas;
* Spring Data JPA;
* Mapeamento de entidades;
* Consultas derivadas do Spring Data;
* Implementação de regras de negócio;
* Integração com banco de dados.

## 🔮 Próximos passos

Algumas evoluções que podem ser adicionadas ao projeto:

* Validação dos dados de entrada;
* Tratamento global de exceções;
* DTOs para entrada e saída de dados;
* Documentação com Swagger/OpenAPI;
* Testes unitários e de integração;
* Autenticação e autorização;
* Migração do H2 para PostgreSQL;
* Validação mais completa de conflitos de horários;
* Paginação e filtros de agendamentos.

## 👨‍💻 Autor

**Vitório Santos**

Projeto desenvolvido para prática e evolução em **desenvolvimento backend com Java e Spring Boot**.

