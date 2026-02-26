<div align="center">

<img src="https://cdn-icons-png.flaticon.com/512/2232/2232688.png" alt="Agenda Estudantil Logo" width="110" />

# 📚 Agenda Estudantil — JSP

**Um sistema web para gestão centralizada de alunos, professores**
**e atividades acadêmicas, desenvolvido com JavaServer Pages.**

<br>

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![JSP](https://img.shields.io/badge/JSP-Servlets-007396?style=for-the-badge&logo=java&logoColor=white)
![Tomcat](https://img.shields.io/badge/Apache%20Tomcat-F8DC75?style=for-the-badge&logo=apachetomcat&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completo-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

## 📚 Tabela de Conteúdos

> Navegue rapidamente pelas seções do projeto.

| # | Seção |
|:-:|:------|
| 1 | [📖 Sobre o Projeto](#-sobre-o-projeto) |
| 2 | [✨ Funcionalidades Principais](#-funcionalidades-principais) |
| 3 | [🛠️ Pilha de Tecnologias](#️-pilha-de-tecnologias) |
| 4 | [🗃️ Estrutura do Banco de Dados](#️-estrutura-do-banco-de-dados) |
| 5 | [📂 Estrutura do Projeto](#-estrutura-do-projeto) |
| 6 | [🚀 Como Executar](#-como-executar) |
| 7 | [🤝 Como Contribuir](#-como-contribuir) |
| 8 | [👨‍💻 Autor](#-autor) |
| 9 | [📄 Licença](#-licença) |

---

## 📖 Sobre o Projeto

> **Agenda Estudantil** é um sistema web acadêmico desenvolvido inteiramente com **JavaServer Pages (JSP)**, focado no ambiente educacional.

A aplicação permite o **registro e a gestão centralizada** de usuários do sistema — professores e alunos — e das suas respectivas atividades acadêmicas, com relacionamentos diretos entre os envolvidos em cada tarefa.

---

## ✨ Funcionalidades Principais

| Ícone | Módulo | Descrição |
|:-----:|:-------|:----------|
| 👨‍🏫 | **Gestão de Professores** | Registro e gerenciamento de professores no sistema acadêmico. |
| 🎓 | **Gestão de Alunos** | Registro e gerenciamento de alunos vinculados ao sistema. |
| 📝 | **Gestão de Atividades** | Registro de atividades com associação direta a alunos e professores responsáveis. |

---

## 🛠️ Pilha de Tecnologias

| Tecnologia | Função no Projeto |
|:-----------|:------------------|
| **Java (JSP / Servlets)** | Linguagem e tecnologia principal para lógica de negócio e renderização server-side. |
| **JavaServer Pages (JSP)** | Geração dinâmica das páginas HTML com dados do servidor. |
| **Apache Tomcat** | Servidor de aplicação Java para deploy e execução do projeto. |
| **MySQL / PostgreSQL** | Banco de dados relacional para persistência dos dados. |
| **HTML5 & CSS3** | Estrutura e estilização das páginas da aplicação. |

---

## 🗃️ Estrutura do Banco de Dados

> O banco de dados é composto por **três tabelas principais** com relacionamentos via chaves estrangeiras.

### 📊 Diagrama de Relacionamento

```
┌─────────────────┐         ┌──────────────────────────┐         ┌───────────────┐
│   professores   │         │        atividades         │         │    alunos     │
│─────────────────│         │──────────────────────────│         │───────────────│
│ id_professor PK │◄────────│ id_professor_resp  FK    │────────►│ id_aluno   PK │
│ nome            │  1    N │ id_aluno_atrib     FK    │ N    1  │ nome          │
│ email           │         │ id_atividade       PK    │         │ email         │
│ senha           │         │ descricao                │         │ senha         │
└─────────────────┘         │ data_entrega             │         └───────────────┘
                            └──────────────────────────┘
```

### 🔧 Script SQL

```sql
-- ─────────────────────────────────────────
-- Tabela: Professores
-- ─────────────────────────────────────────
CREATE TABLE professores (
    id_professor INT PRIMARY KEY AUTO_INCREMENT,
    nome         VARCHAR(255) NOT NULL,
    email        VARCHAR(100) UNIQUE,
    senha        VARCHAR(100)
);

-- ─────────────────────────────────────────
-- Tabela: Alunos
-- ─────────────────────────────────────────
CREATE TABLE alunos (
    id_aluno INT PRIMARY KEY AUTO_INCREMENT,
    nome     VARCHAR(255) NOT NULL,
    email    VARCHAR(100) UNIQUE,
    senha    VARCHAR(100)
);

-- ─────────────────────────────────────────
-- Tabela: Atividades
-- (relaciona professores e alunos)
-- ─────────────────────────────────────────
CREATE TABLE atividades (
    id_atividade      INT PRIMARY KEY AUTO_INCREMENT,
    descricao         TEXT NOT NULL,
    data_entrega      DATE,
    id_professor_resp INT,
    id_aluno_atrib    INT,
    FOREIGN KEY (id_professor_resp) REFERENCES professores(id_professor),
    FOREIGN KEY (id_aluno_atrib)    REFERENCES alunos(id_aluno)
);
```

---

## 📂 Estrutura do Projeto

```plaintext
agenda_jsp/
│
├── 📄 pom.xml / build.gradle          # ⚙️  Configurações de build (Maven ou Gradle)
│
├── 📁 src/
│   └── 📁 main/
│       ├── 📁 java/
│       │   └── 📁 com/agenda/
│       │       ├── 📄 Conexao.java            # 🔌 Configuração da conexão com o banco
│       │       ├── 📁 model/
│       │       │   ├── 📄 Professor.java       # 🏛️  Modelo de Professor
│       │       │   ├── 📄 Aluno.java           # 🏛️  Modelo de Aluno
│       │       │   └── 📄 Atividade.java       # 🏛️  Modelo de Atividade
│       │       ├── 📁 dao/
│       │       │   ├── 📄 ProfessorDAO.java    # 🗃️  Acesso a dados — Professor
│       │       │   ├── 📄 AlunoDAO.java        # 🗃️  Acesso a dados — Aluno
│       │       │   └── 📄 AtividadeDAO.java    # 🗃️  Acesso a dados — Atividade
│       │       └── 📁 servlet/
│       │           ├── 📄 ProfessorServlet.java # 🎛️  Controller — Professor
│       │           ├── 📄 AlunoServlet.java     # 🎛️  Controller — Aluno
│       │           └── 📄 AtividadeServlet.java # 🎛️  Controller — Atividade
│       │
│       └── 📁 webapp/
│           ├── 📄 index.jsp                    # 🏠 Página inicial
│           ├── 📁 professores/
│           │   ├── 📄 cadastro.jsp             # 👨‍🏫 Formulário de cadastro
│           │   └── 📄 lista.jsp                # 📋 Listagem de professores
│           ├── 📁 alunos/
│           │   ├── 📄 cadastro.jsp             # 🎓 Formulário de cadastro
│           │   └── 📄 lista.jsp                # 📋 Listagem de alunos
│           ├── 📁 atividades/
│           │   ├── 📄 cadastro.jsp             # 📝 Formulário de atividade
│           │   └── 📄 lista.jsp                # 📋 Listagem de atividades
│           ├── 📁 css/
│           │   └── 📄 style.css                # 🎨 Folha de estilos
│           └── 📁 WEB-INF/
│               └── 📄 web.xml                  # ⚙️  Configuração do Servlet Container
│
└── 📄 database.sql                    # 🗃️  Script de criação do banco de dados
```

---

## 🚀 Como Executar

### 📋 Pré-requisitos

| Requisito | Detalhe |
|:----------|:--------|
| **JDK** | Versão **11 ou superior** instalada e configurada no `PATH`. |
| **Apache Tomcat** | Versão **9 ou superior** instalada e configurada. |
| **MySQL / PostgreSQL** | Servidor de banco de dados rodando localmente. |
| **IDE** | Recomenda-se **Eclipse IDE for Enterprise Java** ou **IntelliJ IDEA Ultimate**. |
| **Git** | Para clonar o repositório. |

---

### 🔧 Passo a Passo

**1. Clone o repositório:**

```bash
git clone https://github.com/VictorHJesusSantiago/agenda_jsp.git
cd agenda_jsp
```

**2. Configure o banco de dados:**

```bash
# Acesse seu SGBD e execute o script de criação:
mysql -u root -p < database.sql
```

Em seguida, localize o arquivo de conexão (ex: `Conexao.java` ou `config.properties`) e atualize as credenciais:

```java
// Exemplo em Conexao.java
String URL    = "jdbc:mysql://localhost:3306/agenda_jsp";
String USUARIO = "seu_usuario";
String SENHA   = "sua_senha";
```

**3. Compile e gere o arquivo `.war`:**

```bash
# Com Maven
mvn clean install

# Com Gradle
gradle build
```

**4. Faça o deploy no Tomcat:**

```bash
# Copie o .war gerado para a pasta webapps do Tomcat
cp target/agenda_jsp.war /caminho/para/tomcat/webapps/

# Inicie o servidor
/caminho/para/tomcat/bin/startup.sh   # Linux / macOS
/caminho/para/tomcat/bin/startup.bat  # Windows
```

---

### 🛰️ Acesso à Aplicação

| Serviço | URL |
|:--------|:----|
| 🏠 **Página Inicial** | `http://localhost:8080/agenda_jsp` |
| 👨‍🏫 **Professores** | `http://localhost:8080/agenda_jsp/professores` |
| 🎓 **Alunos** | `http://localhost:8080/agenda_jsp/alunos` |
| 📝 **Atividades** | `http://localhost:8080/agenda_jsp/atividades` |

---

## 🤝 Como Contribuir

> Contribuições são muito bem-vindas! Siga as etapas abaixo para colaborar de forma organizada.

| Passo | Ação | Comando |
|:-----:|:-----|:--------|
| 1️⃣ | **Fork** | Crie um fork do repositório para a sua conta. | — |
| 2️⃣ | **Branch** | Crie sua feature branch a partir da `main`. | `git checkout -b feature/NovaFeature` |
| 3️⃣ | **Commit** | Salve as alterações com mensagem clara e semântica. | `git commit -m 'feat: Adiciona NovaFeature'` |
| 4️⃣ | **Push** | Envie a branch para o repositório remoto. | `git push origin feature/NovaFeature` |
| 5️⃣ | **Pull Request** | Abra um PR detalhando as mudanças realizadas. | — |

<div align="center">

<br>

**Se este projeto foi útil para os seus estudos, deixe uma estrela ⭐️ no repositório!**

</div>

---

## 👨‍💻 Autor

<div align="center">

<br>

**Victor H. J. Santiago**

<br>

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/VictorHJesusSantiago)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/victor-henrique-de-jesus-santiago/)

</div>

---

## 📄 Licença

<div align="center">

Este projeto está distribuído sob a **Licença MIT**.
Consulte o arquivo [`LICENSE`](./LICENSE) no repositório para mais informações.

![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

<div align="center">

*Feito com 📚 e Java por **Victor H. J. Santiago***

</div>
