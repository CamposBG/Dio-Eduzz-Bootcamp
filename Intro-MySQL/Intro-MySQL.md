# MySQL

banco de dados -> tabelas (entidades) -> registros ->  campos (coluns)

## Criando banco de dados:

```sql
CREATE DATABASE compras_DB
default character set utf8
default collate utf8_general_ci;
```

## Criar tabelas

Temos que passar os atributos na hora de criar as tabelas, ex:

```sql
use compras_DB;

create table produto (
produto_ID int not null  primary key auto_increment,
nome varchar(30) not null,
valor_unitario decimal (8,2) not null unsigned,
quantidade int not null, 
primary key (produto_ID)
) default charset = utf8;
```

Primary key nao pode se repetir numa tabela

constrains sao regras para criação de coisas, ex. not null

constrins são separadas por espaço 

```sql
use compras_DB;

create table pedido (
pedido_ID int not null auto_increment,
nome_cliente varchar(50) not null,
numer_pedido int unsigned,
email varchar(30) not null,
produtos int,
primary key (pedido_ID)
) default charset = utf8;
```

```sql
use compras_DB;

create table detalhe_pedido (
ID int not null auto_increment,
pedido_ID int,
produto_ID int,
status_pedido enum ('aberto', 'pago', 'cancelado'),
primary key (detalhe_pedido_ID),
foreign key (pedido_ID) REFERENCES pedido  (pedido_ID),
foreign key (produto_ID) REFERENCES produto (produto_ID)
) default charset = utf8;
```

para apagar a tabela mais o conteudo dela

```sql
drop table if exists alunos.
```

modificando linhas

```sql
update nome_da_tabela
set nome = "novo nome", ano = "2015"
where id = "1"
```

deletado redistros (colunas) 

```sql
delte from nome_da_tabela
where id = "2"
```

Removendo todos os registros de uma tabela

```sql
truncate table nome_da_tabela
```

Add dados a tabela

comando ``insert into`` é necessário indicar as colunas que serão preenchidas e os respectivos valores

ex:

```sql
insert into pessoas (nome, nascimento) values (bruno, 1990-12-25)
```

Selecionar e ataulizar dados

Select 

pega as informações de uma tabela especifica



```sql
select * from nome_da_tabela
select nome, nascimento from nome_da_tabela
```

Atualizar os dados

update

alterar as informações 

```sql
update nome_tabla set nome ='novo nome' where id=1;
```

Ordenar os dados

```sql
Select * from nome_tabela order by nome
```

ordenação em forma decrescente:

```sql
Select * from nome_tabela order by nome desc
```

inseringo uma coluna e Agrupamento de informações

ex: alterando qualquer informação na tavela ``alter table``

```sql
alter table nome_tabela add genero varchar(1) not null alter nascimento
```

aqui ele vai agrupar as informações por genero e faz uma contagem de quantos elementos recebem cada genero, ele faz essa contagem pelo id

```sql
select count (id), genrero from pessosa group by genero
```
