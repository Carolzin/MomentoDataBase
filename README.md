# Momento 👩🏻‍💻

Você está prestes a explorar o banco de dados da empresa "Momento"! Com essa base de dados, vamos treinar consultas SQL e responder algumas perguntas intrigantes que vão revelar como a empresa está organizada. Vamos lá?

## Departamento de Tecnologia

Inclua suas próprias informações no departamento de Tecnologia da empresa.

Q:
```sql
INSERT INTO funcionarios (primeiro_nome, sobrenome, email, senha, telefone, data_contratacao, cargo_id, salario, departamento_id) 
VALUES ('Caroline', 'Fernandes', 'carol-28.01@hotmail.com', 'Edsheeranmelhorcantor', '111111111', CURDATE(), 9, 8000.00, 3);
```

Agora diga, quantos funcionários temos ao total na empresa? 
R: 41

Q:
```sql
SELECT COUNT(*) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id;
```

E quanto ao Departamento de Tecnologia?
R: 5

Q: 
```sql
SELECT COUNT(*) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Tecnologia';
```

## Departamento de Vendas

Quantos funcionários trabalham no Departamento de Vendas? Use uma consulta para descobrir o número total de funcionários alocados nesse departamento.
R: 5

Q: 
```sql
SELECT COUNT(*) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Vendas';
```

## Salários no Departamento de Vendas

Qual é o custo total dos salários do pessoal de Vendas? Isso nos ajuda a entender o orçamento do departamento!
R: R$10300.000000

Q:
```sql
SELECT AVG(salario) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Vendas';
```

Quanto o departamento de Vendas gasta em salários?
R: R$51500.00

```sql
SELECT SUM(salario) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Vendas';
```

Quais são os produtos mais vendidos e quais têm pouca ou nenhuma saída?
R: Mais vendido: Uniforme do Superman, 177 unidades.
Produtos com pouco ou nenhuma saída: Iron-man Mk 5 Helmet
R do Robin

Q: 
```sql
SELECT produto_nome 
FROM produtos 
WHERE produto_id NOT IN (SELECT produto_id FROM vendas);
```

Qual é o produto mais caro no inventário da empresa?

## Departamento de Inovações

Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.

O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.

## Funcionários

Quantos funcionários da empresa Momento possuem conjuges?
R: 4

Q:
```sql
SELECT COUNT(DISTINCT funcionario_id) AS funcionarios_com_conjuges 
FROM dependentes 
WHERE relacionamento = 'Cônjuge';
```

Qual o funcionário contratado há mais tempo na empresa?
R: Steven Wayne, 17/06/1987

Q:
```sql
SELECT primeiro_nome, sobrenome, data_contratacao 
FROM funcionarios 
ORDER BY data_contratacao ASC 
LIMIT 1;
```

Qual o funcionário contratado há menos tempo na empresa?
R: Zatana Zatara

Q:
```sql
SELECT primeiro_nome, sobrenome, data_contratacao 
FROM funcionarios 
ORDER BY data_contratacao DESC 
LIMIT 1;
```

Quem são os funcionários com mais tempo na empresa, considerando a data_contratacao?

Como a média salarial dos funcionários da "Momento" evoluiu nos últimos anos? Dica: utilize a função AVG() para calcular a média salarial dos funcionários. e GROUP BY para agrupar os resultados por ano.

Q:
```sql
SELECT YEAR(data_contratacao) AS ano, AVG(salario) AS media_salarial 
FROM funcionarios 
GROUP BY YEAR(data_contratacao) 
ORDER BY ano;
```

## Médias salariais

Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO, CMO e CFO?
R: R$8442.894737

Q:

```sql
SELECT AVG(salario) AS media_salario_executivos 
FROM funcionarios 
WHERE cargo_id NOT IN (SELECT cargo_id FROM cargos WHERE cargo_nome IN ('CEO', 'CMO', 'CFO'));
```



Qual a média salarial do departamento de tecnologia?
R: R$5760.000000

Q:

```sql
SELECT AVG(salario) AS media_salario_tecnologia 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Tecnologia';
```

Qual o departamento com a maior média salarial?
R: Tecnologias Avançadas

Q:

```sql
SELECT departamento_nome, AVG(salario) AS media_salarial 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
GROUP BY departamento_nome 
ORDER BY media_salarial DESC 
LIMIT 1;
```

Qual o departamento com o menor número de funcionários?

## Produtos

Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

Qual o produto mais vendido da empresa?

Qual o produto menos vendido da empresa?

## Escritórios
Quantos escritórios a "Momento" possui em cada região? (Dica: relacione as tabelas regioes e escritorios).

Qual é o custo total de suprimentos em cada escritório? Que tal ordenar os resultados para ver qual escritório possui os suprimentos mais caros?
R:

![image](https://github.com/user-attachments/assets/8623f11e-dcb6-4120-9df0-bdd82031372d)

Q:
```sql
SELECT e.escritorio_nome, SUM(s.custo * s.quantidade) AS custo_total_suprimentos 
FROM escritorios e
JOIN suprimentos s ON e.escritorio_id = s.escritorio_id 
GROUP BY e.escritorio_nome 
ORDER BY custo_total_suprimentos DESC;
```

