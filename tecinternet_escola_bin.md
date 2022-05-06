<!-- Criação do Banco de Dados -->
```sql
CREATE DATABASE tecinternet_escola_bin CHARACTER SET utf8mb4
```

<!-- Criação da tabela "cursos" -->
```sql
CREATE TABLE cursos(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(30) NOT NULL
    cHoraria SMALLINT NOT NULL
    professor_id SMALLINT NULL
)
```

<!-- Criação da tabela "professores" -->
```sql
CREATE TABLE professores(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nomeProfessor VARCHAR(30) NOT NULL
    materia ENUM("design","desenvolvimento","infra") NOT NULL
    cursos_id SMALLINT NULL
)
```

<!-- Criação da tabela "alunos" -->
```sql
CREATE TABLE alunos(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nomeAluno VARCHAR(50) NOT NULL
    nascimento DATE NOT NULL
    nota1 DECIMAL(4,2) NOT NULL
    nota2 DECIMAL(4,2) NOT NULL
    cursos_id SMALLINT NULL
)
```