<!-- Criação do Banco de Dados -->
```sql
CREATE DATABASE tecinternet_escola_bin CHARACTER SET utf8mb4
```

<!-- Criação da tabela "cursos" -->
```sql
CREATE TABLE cursos(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(30) NOT NULL,
    cHoraria SMALLINT NOT NULL,
    professor_id SMALLINT NULL
)
```

<!-- Criação da tabela "professores" -->
```sql
CREATE TABLE professores(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nomeProfessor VARCHAR(30) NOT NULL,
    materia ENUM("design","desenvolvimento","infra") NOT NULL,
    cursos_id SMALLINT NOT NULL
)
```

<!-- Criação da tabela "alunos" -->
```sql
CREATE TABLE alunos(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nomeAluno VARCHAR(50) NOT NULL,
    nascimento DATE NOT NULL,
    nota1 DECIMAL(4,2) NOT NULL,
    nota2 DECIMAL(4,2) NOT NULL,
    cursos_id SMALLINT NOT NULL
)
```

<!-- Criando relações entre as tabelas -->
```sql
-- Relação professor_id-cursos
ALTER TABLE cursos
    ADD CONSTRAINT fk_cursos_professores

    FOREIGN KEY (professor_id) REFERENCES professores(id)

-- Relação cursos_id-professores
ALTER TABLE professores
    ADD CONSTRAINT fk_professores_cursos

    FOREIGN KEY (cursos_id) REFERENCES cursos(id)

-- Relação cursos_id-alunos
ALTER TABLE alunos
    ADD CONSTRAINT fk_alunos_cursos

    FOREIGN KEY (cursos_id) REFERENCES cursos(id)
```

### Cadastrando cursos
```sql
INSERT INTO cursos (titulo, cHoraria, professor_id) VALUES
("Front-End",
"40h",
NULL),
("Back-end",
"80h",
NULL),
("UX/UI Design",
"30h",
NULL),
("Figma",
"10h",
NULL),
("Redes de Computadores",
"100h",
NULL)
```

### Cadastrando professores
```sql
INSERT INTO professores (nomeProfessor, materia, cursos_id) VALUES
("Jon Oliva",
"Infra",
25),
("Lemmy Kilmister",
"Design",
24),
("Neil Peart",
"Design",
23),
("Ozzy Osbourne",
"Desenvolvimento",
22),
("David Gilmour",
"Desenvolvimento",
21)
```


### Atualizando dados da tabela
```sql
UPDATE cursos SET professor_id = 5 WHERE id=21;
UPDATE cursos SET professor_id = 4 WHERE id=22;
UPDATE cursos SET professor_id = 3 WHERE id=23;
UPDATE cursos SET professor_id = 2 WHERE id=24;
UPDATE cursos SET professor_id = 1 WHERE id=25;
```