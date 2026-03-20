# Roteiro Completo de Banco de Dados

## Objetivo
Executar todas as operações essenciais em SQL com passo a passo.

---

## 1. Criar banco

```sql
CREATE DATABASE faculdade_db;
USE faculdade_db;
```

---

## 2. Criar tabelas

```sql
CREATE TABLE cursos (
    id_curso INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    carga_horaria INT NOT NULL
);

CREATE TABLE alunos (
    id_aluno INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    data_nascimento DATE,
    id_curso INT,
    FOREIGN KEY (id_curso) REFERENCES cursos(id_curso)
);

CREATE TABLE disciplinas (
    id_disciplina INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    carga_horaria INT NOT NULL
);

CREATE TABLE matriculas (
    id_matricula INT PRIMARY KEY AUTO_INCREMENT,
    id_aluno INT NOT NULL,
    id_disciplina INT NOT NULL,
    data_matricula DATE NOT NULL,
    nota DECIMAL(4,2),
    FOREIGN KEY (id_aluno) REFERENCES alunos(id_aluno),
    FOREIGN KEY (id_disciplina) REFERENCES disciplinas(id_disciplina)
);
```

---

## 3. Inserção de dados

```sql
INSERT INTO cursos (nome, carga_horaria)
VALUES ('Engenharia de Computação', 3600),
       ('Sistemas de Informação', 3200);

INSERT INTO alunos (nome, email, data_nascimento, id_curso)
VALUES ('Ana', 'ana@email.com', '2002-05-10', 1),
       ('Bruno', 'bruno@email.com', '2001-09-21', 2);

INSERT INTO disciplinas (nome, carga_horaria)
VALUES ('Banco de Dados', 60),
       ('Web', 80);

INSERT INTO matriculas (id_aluno, id_disciplina, data_matricula, nota)
VALUES (1, 1, '2026-03-20', 8.5),
       (2, 2, '2026-03-20', 7.0);
```

---

## 4. Consultas

```sql
SELECT * FROM alunos;

SELECT nome FROM alunos;

SELECT * FROM alunos WHERE id_curso = 1;

SELECT * FROM matriculas WHERE nota >= 8;

SELECT * FROM alunos ORDER BY nome ASC;

SELECT * FROM alunos LIMIT 1;
```

---

## 5. Filtros avançados

```sql
SELECT * FROM alunos WHERE nome LIKE 'A%';

SELECT * FROM matriculas WHERE nota BETWEEN 7 AND 9;

SELECT * FROM alunos WHERE id_aluno IN (1,2);

SELECT * FROM matriculas WHERE nota IS NULL;
```

---

## 6. UPDATE

```sql
UPDATE alunos
SET email = 'novo@email.com'
WHERE id_aluno = 1;
```

---

## 7. DELETE

```sql
DELETE FROM matriculas
WHERE id_matricula = 1;
```

---

## 8. Agregações

```sql
SELECT COUNT(*) FROM alunos;

SELECT AVG(nota) FROM matriculas;

SELECT MAX(nota), MIN(nota) FROM matriculas;
```

---

## 9. GROUP BY

```sql
SELECT id_disciplina, AVG(nota)
FROM matriculas
GROUP BY id_disciplina;
```

---

## 10. JOIN

```sql
SELECT a.nome, c.nome
FROM alunos a
JOIN cursos c ON a.id_curso = c.id_curso;

SELECT a.nome, d.nome, m.nota
FROM matriculas m
JOIN alunos a ON m.id_aluno = a.id_aluno
JOIN disciplinas d ON m.id_disciplina = d.id_disciplina;
```

---

## 11. ALTER TABLE

```sql
ALTER TABLE alunos ADD telefone VARCHAR(20);

ALTER TABLE alunos DROP COLUMN telefone;
```

---

## 12. VIEW

```sql
CREATE VIEW vw_notas AS
SELECT a.nome, m.nota
FROM alunos a
JOIN matriculas m ON a.id_aluno = m.id_aluno;
```

---

## 13. INDEX

```sql
CREATE INDEX idx_nome ON alunos(nome);
```

---

## 14. TRANSAÇÕES

```sql
START TRANSACTION;

UPDATE matriculas SET nota = 10 WHERE id_matricula = 2;

ROLLBACK;

START TRANSACTION;

UPDATE matriculas SET nota = 10 WHERE id_matricula = 2;

COMMIT;
```

---

## 15. DDL / DML / DQL / TCL

- DDL: CREATE, ALTER, DROP
- DML: INSERT, UPDATE, DELETE
- DQL: SELECT
- TCL: COMMIT, ROLLBACK

---

## 16. Desafio

- Criar novo banco
- Criar 5 tabelas
- Inserir dados
- Fazer JOIN
- Criar VIEW
- Criar INDEX
- Usar TRANSAÇÃO

---
