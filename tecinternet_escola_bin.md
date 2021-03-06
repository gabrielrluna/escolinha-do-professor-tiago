### Criação do Banco de Dados
```sql
CREATE DATABASE tecinternet_escola_bin CHARACTER SET utf8mb4
```

### Criação da tabela "cursos"
```sql
CREATE TABLE cursos(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(30) NOT NULL,
    cHoraria SMALLINT NOT NULL,
    professor_id SMALLINT NULL
)
```

### Criação da tabela "professores"

```sql
CREATE TABLE professores(
    id SMALLINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nomeProfessor VARCHAR(30) NOT NULL,
    materia ENUM("design","desenvolvimento","infra") NOT NULL,
    cursos_id SMALLINT NOT NULL
)
```

### Criação da tabela "alunos"
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

### Criando relações entre as tabelas

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
40,
NULL),
("Back-end",
80,
NULL),
("UX/UI Design",
30,
NULL),
("Figma",
10,
NULL),
("Redes de Computadores",
100,
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

### Cadastrando alunos na escola

```sql
INSERT INTO alunos (nomeAluno, nascimento, nota1, nota2, cursos_id) VALUES
("Bertoldo Bredtch",
"2000-05-23",
10.00,
8.56,
21),
("Dona Cacilda",
"1996-11-28",
9.65,
5.65,
22),
("Aldemar Vigário",
"1950-09-11",
7.45,
2.15,
23),
("Seu Boneco",
"1990-06-20",
4.98,
9.36,
23),
("Dona Catifunda",
"1995-07-12",
6.78,
8.45,
23),
("Rolando Lero",
"1976-01-15",
1.45,
0.32,
23),
("Paulo Cintura",
"1986-10-29",
4.82,
9.76,
24),
("Dona Flor",
"2001-03-12",
10.00,
10.00,
24),
("Armando Volta",
"1998-07-01",
5.03,
9.45,
25),
("Galeão Cumbica",
"1993-12-12",
8.23,
2.94,
21)
```


### Consultando os alunos que nasceram antes de 1995

```SQL
SELECT nomeAluno, nascimento FROM alunos WHERE nascimento < "1999-01-01";
```

### Consultando a média das notas dos alunos

```SQL
SELECT nomeAluno, ROUND(AVG(nota1+nota2)/2, 2) AS "Média Final" FROM alunos GROUP BY nomeAluno;
```

### Criando limite de carga horária dos cursos
```SQL
SELECT titulo, cHoraria, ROUND(cHoraria*0.25)AS "Limite de Faltas" FROM cursos ORDER BY titulo
```

### Consultando professores de desenvolvimento

```sql
SELECT nomeProfessor, materia FROM professores WHERE materia = "desenvolvimento";
```

### Contando os professores de desenvolvimento
```sql
SELECT COUNT(materia) AS "Quantidade de professores" FROM professores WHERE materia = "desenvolvimento"
```


### Consultando nome dos alunos, o título e a carga horária dos cursos

```sql
SELECT alunos.nomeAluno, cursos.titulo, cursos.cHoraria
FROM alunos INNER JOIN cursos
ON alunos.cursos_id = cursos.id;
```

# Consultando professores e seus respectivos cursos

```sql
SELECT professores.nomeProfessor, cursos.titulo FROM professores INNER JOIN cursos
ON professores.cursos_id = cursos.id;
```

# Consultando professores e seus respectivos cursos

```sql
SELECT alunos.nomeAluno, cursos.titulo, professores.nomeProfessor
FROM alunos
LEFT JOIN cursos ON alunos.cursos_id = cursos.id
LEFT JOIN professores ON professores.cursos_id = cursos.id;
```



### Contando a quantidade de alunos por curso

```sql
SELECT cursos.titulo AS Matéria,
COUNT(alunos.cursos_id) AS "Alunos"
FROM alunos LEFT JOIN cursos ON alunos.cursos_id = cursos.id
GROUP BY Matéria
```

###  Fazendo uma consulta que mostre o nome dos alunos, suas notas, médias, e o título dos cursos que fazem. Devem ser considerados somente os alunos de Front-End e Back-End,classificados pelo nome do aluno.


```sql
SELECT nomeAluno, cursos.titulo AS "Curso", nota1, nota2, ROUND(AVG(nota1+nota2)/2, 2) AS "Média Final"
FROM alunos LEFT JOIN cursos ON alunos.cursos_id = cursos.id
WHERE cursos.id = 21 or cursos.id = 22
GROUP BY nomeAluno 
ORDER BY nomeAluno
```


### Consulta que altera o nome do curso de Figma para Adobe XD e sua carga horária de 10 para 15

```sql
UPDATE cursos SET titulo = "Adobe XD" WHERE id=24
UPDATE cursos SET cHoraria = 15 WHERE id = 24;
```


### Excluindo um aluno do curso de Redes de Computadores e um aluno do curso de UX/UI.

```sql
DELETE FROM alunos WHERE id = 12 OR id=8
```

### Lista de alunos atualizada e o título dos cursos que fazem, classificados pelo nome do aluno.

```sql
SELECT alunos.nomeAluno, cursos.titulo
FROM alunos INNER JOIN cursos
ON alunos.cursos_id = cursos.id;
ORDER BY nomeAluno
```


## HORA DO DESAFIO, GALERA!

### Criar uma consulta que calcule a idade do aluno

```SQL
SELECT nomeAluno, nascimento, (2022 - (YEAR(nascimento)))
AS "Idade"
FROM alunos
```

### Criar uma consulta que calcule a média das notas de cada aluno e mostre somente os alunos que tiveram a média maior ou igual a 7.

```SQL
SELECT nomeAluno, ROUND(AVG(nota1+nota2)/2, 2) AS "Média" FROM alunos WHERE ((nota1+nota2)/2) <= 7 GROUP BY nomeAluno;
```

### Criar uma consulta que calcule a média das notas de cada aluno e mostre somente os alunos que tiveram a média menor que 7.

```SQL
SELECT nomeAluno, ROUND(AVG(nota1+nota2)/2, 2) AS "Média" FROM alunos WHERE ((nota1+nota2)/2) <= 7 GROUP BY nomeAluno;
```

### Criar uma consulta que mostre a quantidade de alunos com média maior ou igual a 7.
```SQL
SELECT COUNT((nota1+nota2)/2) AS "Quantidade de Alunos"
FROM alunos 
WHERE((nota1+nota2)/2) >= 7;
```
