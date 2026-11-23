# API Clínica Odontológica

## 1. Nome e Descrição do Projeto

**API Clínica Odontológica** é uma aplicação full-stack desenvolvida para o gerenciamento administrativo e operacional de clínicas odontológicas. O sistema integra uma API RESTful construída em Spring Boot a uma interface web de página única (SPA), permitindo o controle completo de cadastros e o agendamento inteligente de consultas.

---

## 2. Problema Atendido, Público Usuário e Funcionalidades

### Problema Atendido
Clínicas odontológicas de pequeno e médio porte frequentemente enfrentam dificuldades no controle manual de agendas, resultando em choque de horários entre profissionais, ocupação simultânea da mesma sala de atendimento e descentralização dos dados de pacientes e procedimentos. O sistema resolve esse problema centralizando os cadastros e validando automaticamente a disponibilidade de dentistas e consultórios no momento do agendamento.

### Público Usuário
* **Recepcionistas e Secretárias:** Responsáveis pelo cadastro de pacientes, controle de disponibilidade das salas e marcação, alteração ou cancelamento de consultas.
* **Gestores e Administradores da Clínica:** Responsáveis pelo gerenciamento do corpo clínico (dentistas), catálogo de procedimentos e estrutura de consultórios.

### Funcionalidades
* **Gestão de Pacientes:** Cadastro, consulta, atualização e exclusão de pacientes (nome, CPF, telefone, e-mail e data de nascimento).
* **Gestão de Dentistas:** Controle de profissionais com validação de registro (CRO) e especialidade.
* **Catálogo de Procedimentos:** Cadastro de serviços odontológicos com definição de valor e duração estimada em minutos.
* **Controle de Consultórios:** Gerenciamento das salas físicas de atendimento e seus status de disponibilidade.
* **Agendamento de Consultas:** Marcação de atendimentos vinculando paciente, dentista, procedimento e consultório, com bloqueio automático de datas retroativas e validação de conflitos de horário (tanto para o dentista quanto para o consultório, calculados a partir da duração do procedimento).

---

## 3. Tecnologias Utilizadas

* **Linguagem e Back-end:** Java 21, Spring Boot, Spring Web, Spring Data JPA, Jakarta Bean Validation
* **Banco de Dados:** MySQL 8
* **Gerenciador de Dependências:** Apache Maven
* **Front-end:** HTML5, CSS3 e JavaScript (Vanilla JS — SPA)
* **Controle de Versão:** Git e GitHub

---

## 4. Pré-requisitos e Instruções de Instalação e Execução

### Pré-requisitos
* **Java Development Kit (JDK):** Versão 17 ou superior (recomendado JDK 21)
* **MySQL Server:** Versão 8.0 ou superior
* **Maven:** Versão 3.8+ (ou uso do Maven Wrapper `./mvnw` incluso no projeto)
* **Navegador Web moderno:** Chrome, Edge, Firefox ou similar

### Instalação e Execução

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/VictorCorrea-dev/api-clinicaOdonto.git
   cd api-clinicaOdonto
   ```

2. **Configure o banco de dados e as variáveis de ambiente** (conforme detalhado na seção 5).

3. **Execute o Back-end (API):**
   * Pelo terminal, na raiz do projeto, execute:
     ```bash
     ./mvnw spring-boot:run
     ```
   * Ou abra o projeto em sua IDE Java (IntelliJ IDEA, Eclipse ou VS Code) e execute a classe principal `ClinicaOdontoApplication.java`.

4. **Execute o Front-end:**
   * Navegue até a pasta do front-end do projeto e abra o arquivo `index.html` diretamente no navegador (ou utilize uma extensão como *Live Server*).

---

## 5. Configuração do Banco de Dados e Variáveis de Ambiente

1. Certifique-se de que o serviço do **MySQL** esteja ativo em sua máquina. O banco de dados `clinica_odonto` será criado automaticamente na primeira execução caso não exista.

2. Defina as seguintes variáveis de ambiente no seu sistema operacional ou na configuração de execução da sua IDE (não insira senhas reais diretamente no código-fonte):

   | Variável de Ambiente | Descrição | Exemplo de Valor |
   | :--- | :--- | :--- |
   | `DB_URL` | URL de conexão JDBC com o MySQL | `jdbc:mysql://localhost:3306/clinica_odonto?createDatabaseIfNotExist=true` |
   | `DB_USERNAME` | Usuário do banco de dados MySQL | `seu_usuario_mysql` |
   | `DB_PASSWORD` | Senha do banco de dados MySQL | `sua_senha_segura` |

3. No arquivo `src/main/resources/application.properties`, as propriedades referenciam essas variáveis de forma segura:
   ```properties
   spring.datasource.url=${DB_URL:jdbc:mysql://localhost:3306/clinica_odonto?createDatabaseIfNotExist=true}
   spring.datasource.username=${DB_USERNAME:root}
   spring.datasource.password=${DB_PASSWORD:}
   spring.jpa.hibernate.ddl-auto=update
   spring.jackson.deserialization.fail-on-null-for-primitives=false
   ```

---

## 6. Endereço Base e Resumo dos Endpoints da API

* **Endereço Base (Local):** `http://localhost:8080`

Todas as entidades disponibilizam operações RESTful padronizadas:

### Recursos Disponíveis
* `/pacientes` — Gerenciamento de pacientes
* `/dentistas` — Gerenciamento de dentistas
* `/procedimentos` — Gerenciamento de procedimentos odontológicos
* `/consultorios` — Gerenciamento de consultórios
* `/agendamentos` — Gerenciamento de agendamentos de consultas

### Resumo das Rotas

| Método HTTP | Endpoint | Descrição | Status de Sucesso |
| :--- | :--- | :--- | :--- |
| `GET` | `/{recurso}` | Retorna a lista de todos os registros cadastrados | `200 OK` |
| `GET` | `/{recurso}/{id}` | Busca e retorna um registro específico pelo seu ID | `200 OK` |
| `POST` | `/{recurso}` | Cria um novo registro a partir do corpo JSON enviado | `201 Created` |
| `PUT` | `/{recurso}/{id}` | Atualiza os dados de um registro existente | `200 OK` |
| `DELETE` | `/{recurso}/{id}` | Exclui permanentemente um registro pelo seu ID | `204 No Content` |

---

## 7. Instruções para Executar os Testes ou Usar a Coleção de Requisições

### Execução de Testes Automatizados
Para executar a suíte de testes unitários e de contexto do Spring Boot via terminal:
```bash
./mvnw test
```

### Testes Manuais e Coleção de Requisições (Postman / Insomnia)
1. Com a API em execução em `http://localhost:8080`, abra o **Postman**, **Insomnia** ou o próprio **Front-end (`index.html`)**.
2. Cadastre primeiro os registros base (`POST /pacientes`, `POST /dentistas`, `POST /procedimentos` e `POST /consultorios`).
3. Para testar a criação de um agendamento (`POST http://localhost:8080/agendamentos`), utilize o seguinte exemplo de corpo JSON (`Content-Type: application/json`):
   ```json
   {
     "dataHora": "2026-12-10T14:30:00",
     "observacoes": "Avaliação inicial",
     "paciente": { "id": 1 },
     "dentista": { "id": 1 },
     "procedimento": { "id": 1 },
     "consultorio": { "id": 1 }
   }
   ```
4. Para validar a regra de conflito de horário, tente enviar uma segunda requisição `POST /agendamentos` no mesmo horário para o mesmo `dentista` ou `consultorio` — a API retornará erro impedindo a sobreposição.

---

## 8. Créditos e Recursos Externos Utilizados

* **Spring Framework / Spring Boot:** Utilizado como base estrutural para a API REST, injeção de dependências, validação e persistência de dados ([spring.io](https://spring.io/)).
* **MySQL Connector/J:** Driver oficial utilizado para comunicação entre a aplicação Java e o banco de dados MySQL.
* **Google Fonts (Inter / Sans-serif):** Tipografia utilizada na estilização da interface web.
* **Autoria:** Projeto desenvolvido por **Victor Correa** ([GitHub](https://github.com/VictorCorrea-dev)) para fins acadêmicos.
