# O Caderno Mágico do Banco de Dados! 🪄📚

Imagine que o **Banco de Dados** é um caderno mágico super inteligente onde guardamos informações. Nesses códigos, nós aprendemos a dar ordens para ele!

## 1. Desenhando as Linhas no Caderno 📖
Primeiro, precisamos criar um espaço especial para anotar as coisas. Usamos um feitiço chamado `CREATE TABLE`. É como desenhar uma tabela com régua no caderno, separando um lugar para o número, o nome do aluno, a sala dele e a nota que ele tirou.

```sql
CREATE TABLE alunos10(
    id NUMBER PRIMARY KEY,
    nome VARCHAR2(30),
    turma VARCHAR2(30),
    nota NUMBER
);
```

## 2. Escrevendo com a Caneta Mágica ✍️
Agora que temos a tabela pronta, como colocamos o nome de alguém lá? Usamos o `INSERT INTO`! É como pegar a caneta e escrever na linha. 

Mas para ficar mais rápido, nós criamos um robô ajudante chamado **Procedure** (`prd_insert_alunos`). Toda vez que chamamos esse robô, ele já sabe exatamente como escrever o nome, a turma e a nota no caderno para a gente!

```sql
-- Criando o robô ajudante
CREATE OR REPLACE PROCEDURE prd_insert_alunos (
    p_id NUMBER, p_nome VARCHAR2, p_turma VARCHAR2, p_nota NUMBER
) AS
BEGIN
    INSERT INTO alunos10 (id, nome, turma, nota) 
    VALUES (p_id, p_nome, p_turma, p_nota);
    COMMIT;
END;
```

Para usar o robô e pedir para ele anotar a nota 10 para a aluna Manu, é só fazer assim:
```sql
CALL prd_insert_alunos(1, 'Manu', '2TDSPG', 10);
```

## 3. Lendo o Caderno 👓
Se a gente quiser ver tudo o que está escrito no caderno, usamos uma palavra mágica muito famosa: `SELECT`.
```sql
SELECT * FROM alunos10;
```
Isso faz o caderno mostrar todas as anotações na hora!

## 4. A Calculadora Automática 🤖🧮
E se a gente quiser saber qual foi a nota final (a média) da Manu no boletim? 
Em vez de contar nos dedos, nós ensinamos o caderno a calcular sozinho criando uma **Function** (Função). 

É como dar uma calculadora pro caderno. A gente só passa o nome "Manu" e o caderno devolve a continha pronta!

```sql
-- Criando a calculadora de médias
CREATE FUNCTION media_alunos(nome VARCHAR) RETURN NUMBER IS
    v_media NUMBER;
BEGIN
    SELECT AVG(nota) INTO v_media FROM alunos10 GROUP BY nome; 
    RETURN v_media;
END;
```

E para pedir o resultado para a calculadora, a gente faz a perguntinha final:
```sql
SELECT media_alunos('Manu') FROM dual;
```
E pronto! A mágica acontece e ele te dá a resposta certa. ✨
