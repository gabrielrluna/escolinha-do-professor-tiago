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

