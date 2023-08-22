## ETAPA 1: foi feito pela interface do PhpMyAdmin

## ETAPA 2:

```sql

-- Cadastrando 5 Cursos 
INSERT INTO cursos (titulo, carga_horaria)
VALUES
    ('Front-End', 40),
    ('Back-End', 80),
    ('UX/UI Design', 30),
    ('Figma', 10),
    ('Redes de Computadores', 100);

-- Cadastrando 5 Professores
INSERT INTO professor (nome, area_de_atuacao, curso_id)
VALUES
    ('Jon Oliva', 'infra', 5),
    ('Lemmy Kilmister', 'design', 4),
    ('Neil Peart', 'design', 3),
    ('Ozzy Osbourne', 'desenvolvimento', 2),
    ('David Gilmour', 'desenvolvimento', 1);

-- Atualizando os dados da professor_id

UPDATE cursos SET professor_id = 10 WHERE id = 1;
UPDATE cursos SET professor_id =  9 WHERE id = 2;
UPDATE cursos SET professor_id =  8 WHERE id = 3;
UPDATE cursos SET professor_id =  7 WHERE id = 4;
UPDATE cursos SET professor_id =  6 WHERE id = 5; 


-- Adicionando 10 alunos, com duas notas, data de nascimento e nomes.

INSERT INTO alunos (nome, curso_id, primeira_nota, segunda_nota, data_de_nascimento)
VALUES
    ('Samuel José', 1, 8.0, 9.0, '1983-08-10'),
    ('Pedro Vasconcelos', 2, 6.0, 8.0, '1998-07-20'),
    ('Sofia Peixoto', 5, 3.0, 4.0, '1996-11-10'),
    ('Jhonatan Vinicus', 3, 10.0, 5.5, '1999-02-05'),
    ('Johhny Sans', 4, 5.0, 8.0, '1997-09-25'),
    ('Victor Bueno', 2, 10.0, 10.0, '2006-10-27'),
    ('Rodolfo Machado', 5, 2.0, 3.5, '1995-01-12'),
    ('Nathalia Mota', 1, 6.0, 9.0, '1993-10-30'),
    ('Julia Mota', 2, 6.5, 8.0, '2001-01-13'),
    ('Isaque Silva', 3, 9.0, 10.0, '2013-06-26');
```

## ETAPA 3:

```sql
-- 1- Faça uma consulta que mostre os alunos que nasceram antes do ano 2009
SELECT nome, data_de_nascimento
FROM alunos
WHERE YEAR(data_de_nascimento) < 2009;
```
![print do exercício 01](/imagens/exercicio-01.png)

```sql
-- 2- Faça uma consulta que calcule a média das notas de cada aluno e as mostre com duas casas decimais.
SELECT nome, ROUND((primeira_nota + segunda_nota) / 2, 2) AS 'Média'
FROM alunos;
```
![print do exercício 02](/imagens/exercicio-02.png)

```sql
-- 3- Faça uma consulta que calcule o limite de faltas de cada curso de acordo com a carga horária. Considere o limite como 25% da carga horária. Classifique em ordem crescente pelo título do curso.
SELECT titulo, ROUND(carga_horaria * 0.25) AS 'Lmt De Faltas'
FROM cursos
GROUP BY titulo
ORDER BY titulo;
```
![print do exercício 03](/imagens/exercicio-03.png)

```sql
-- 4- Faça uma consulta que mostre os nomes dos professores que são somente da área "desenvolvimento".
SELECT nome
FROM professor
WHERE area_de_atuacao = 'desenvolvimento';
```
![print do exercício 04](/imagens/exercicio-04.png)

```sql
-- 5- Faça uma consulta que mostre a quantidade de professores que cada área ("design", "infra", "desenvolvimento") possui.
SELECT area_de_atuacao, COUNT(*) AS Quantidade
FROM professor
WHERE area_de_atuacao IN ('design', 'infra', 'desenvolvimento')
GROUP BY area_de_atuacao;
```
![print do exercício 05](/imagens/exercicio-05.png)

```sql
-- 6- Faça uma consulta que mostre o nome dos alunos, o título e a carga horária dos cursos que fazem.
SELECT alunos.nome AS Alunos, cursos.titulo AS Cursos, cursos.carga_horaria
FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id;
```
![print do exercício 06](/imagens/exercicio-06.png)

```sql
-- 7- Faça uma consulta que mostre o nome dos professores e o título do curso que lecionam. Classifique pelo nome do professor.
SELECT professor.nome AS Professor, cursos.titulo AS Cursos
FROM professor 
INNER JOIN cursos ON professor.curso_id = cursos.id
ORDER BY professor;
```
![print do exercício 07](/imagens/exercicio-07.png)

```sql
-- 8- Faça uma consulta que mostre o nome dos alunos, o título dos cursos que fazem, e o professor de cada curso.
SELECT alunos.nome AS Aluno, cursos.titulo AS Curso, professor.nome AS Professor 
FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id
INNER JOIN professor ON cursos.professor_id = professor.id;
```
![print do exercício 08](/imagens/exercicio-08.png)

```sql
-- 9- Faça uma consulta que mostre a quantidade de alunos que cada curso possui. Classifique os resultados em ordem descrecente de acordo com a quantidade de alunos.
SELECT alunos.nome AS Alunos, cursos.titulo AS Curso, professor.nome AS Professor 
FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id
INNER JOIN professor ON cursos.professor_id = professor.id;
```
![print do exercício 09](/imagens/exercicio-09.png)

```sql
-- 10- Faça uma consulta que mostre a quantidade de alunos que cada curso possui. Classifique os resultados em ordem descrecente de acordo com a quantidade de alunos.
SELECT cursos.titulo AS Curso, COUNT(alunos.curso_id) AS Quantidade
FROM cursos
LEFT JOIN alunos ON cursos.id = alunos.curso_id
GROUP BY cursos.titulo
ORDER BY Quantidade DESC;
```
![print do exercício 10](/imagens/exercicio-10.png)

```sql
-- 11- Faça uma consulta que mostre o nome dos alunos, suas notas, médias, e o título dos cursos que fazem. Devem ser considerados somente os alunos de Front-End e Back-End. Mostre os resultados classificados pelo nome do aluno.
SELECT alunos.nome AS Alunos,alunos.primeira_nota AS 'Nota 1', alunos.segunda_nota AS 'Nota 2', ROUND((primeira_nota + segunda_nota) / 2, 2) AS 'Média', cursos.titulo AS Curso
FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id
WHERE cursos.id IN(1,2)
ORDER BY Alunos;
```
![print do exercício 11](/imagens/exercicio-11.png)

```sql
-- 12- Faça uma consulta que altere o nome do curso de Figma para Adobe XD e sua carga horária de 10 para 15.
UPDATE cursos
SET titulo = 'Adobe XD', carga_horaria = 15
WHERE id = 4;
```
## sem print do exercício acima

```sql
-- 13- Faça uma consulta que exclua um aluno do curso de Redes de Computadores e um aluno do curso de UX/UI.
DELETE FROM alunos
WHERE (id = 7 AND curso_id = 5) OR
      (id = 10 AND curso_id = 3);
```
## sem print do exercício acima

```sql
--  Faça uma consulta que mostre a lista de alunos atualizada e o título dos cursos que fazem, classificados pelo nome do aluno.
SELECT alunos.nome AS Aluno, cursos.titulo AS Curso
FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id
ORDER BY Aluno;
```
![print do exercício 13](/imagens/exercicio-13.png)

## DESAFIOS 

### 1:
```sql
SELECT nome, TIMESTAMPDIFF(YEAR, data_de_nascimento, NOW()) AS idade
FROM alunos;
```
![print do desafio 1](/imagens/desafio1.png)

### 2:
```sql
SELECT nome, ROUND((primeira_nota + segunda_nota) / 2, 2) media FROM alunos HAVING media >= 7;
-- evitar repetição da expressão HAVING
```
![print do desafio 2](/imagens/desafio2.png)

### 3:
```sql
SELECT nome, ROUND((primeira_nota + segunda_nota) / 2, 2) media FROM alunos HAVING media < 7;
```
![print do desafio 3](/imagens/desafio3.png)

### 4:
```sql
SELECT COUNT(*) AS 'Quantidade Alunos'
FROM alunos 
WHERE ROUND((primeira_nota + segunda_nota) / 2, 2)  >= 7;
```
![print do desafio 4](/imagens/desafio4.png)
