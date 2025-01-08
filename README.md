# Banco-de-Dados-SQL-SIS-PROMO-O-
Desenvolvimento de Banco de Dados
create database sys_promocao;
show databases;
drop database information_schema;
use sys_promocao;
show tables;
ALTER TABLE tbl_cliente CHANGE COLUMN id id_cliente INT NOT NULL AUTO_INCREMENT;

create table tbl_cliente (
id_cliente int not null primary key auto_increment,
nome_cliente varchar(200) not null,
rg_cliente int not null,
data_nascimento varchar(45) not null,
e_mail varchar (200) not null
);

create table tbl_produto (
id_Produto int not null primary key auto_increment,
nome_produto varchar(100) not null,
quantidade_estoque int not null,
codigo int not null,
valor_compra float not null,
valor_venda float not null,
categoria varchar(100) not null
);

create table tbl_fornecedor (
id_fornecedor int not null primary key auto_increment,
nome_fornecedor varchar(100) not null,
nome_representante varchar(100) not null,
logradouro varchar(100) not null,
cep varchar(100) not null,
bairro varchar(100) not null,
cidade varchar(100) not null,
estado varchar(100) not null,
pais varchar(100) not null
);

create table tbl_colaborador (
id_coladorador int not null primary key auto_increment,
nome varchar(150) not null,
rg varchar (50) not null,
turno varchar(50) not null,
departamento varchar(100) not null,
admissão varchar(100) not null,
cargo varchar (100)not null,

id_cliente int,
constraint fk_tbl_colaborador_tbl_cliente
foreign key (id_cliente)
references sys_promocao.tbl_cliente(id_cliente)
);

create table tbl_compra (
id_compra int not null primary key auto_increment,
data_compras date not null,
total_compras int not null,
credito float not null,
pix float not null,
debito float not null,
dinheiro float not null,

id_cliente int,
constraint fk_tbl_compra_cliente
foreign key (id_cliente)
references sys_promocao.tbl_cliente(id_cliente),

id_Produto int,
constraint fk_tbl_compra_tbl_produto
foreign key (id_produto)
references sys_promocao.tbl_produto(id_produto)
);

create table tbl_endereco (
id_endereco int not null primary Key auto_increment,
cep varchar(20)not null,
logradouro varchar(200),
bairro varchar(200),
cidade varchar (200),
estado varchar(200),
pais varchar(100),

id_cliente int,
constraint fk_tbl_endereco_cliente
foreign key (id_cliente)
references sys_promocao.tbl_cliente(id_cliente)
);

create table tbl_telefone (
id_telefone int not null auto_increment primary key,
telefone varchar(300) not null,

id_cliente int,
constraint fk_tbl_telefone_cliente
foreign key (id_cliente)
references sys_promocao.tbl_cliente(id_cliente)
);

create table tbl_vendas(
id_vendas int not null auto_increment primary key,
total_de_vendas int not null,
data_vendas date not null,
total_credito float not null,
total_pix float not null,
total_debito float not null,
total_dinheiro float not null,
quantidade int not null,
preco float not null,
departamento varchar(200) not null,

id_Produto int,
constraint fk_tbl_vendas_tbl_produto
foreign key (id_produto)
references sys_promocao.tbl_produto(id_produto)
);

create table tbl_estoque(
id_estoque int not null auto_increment primary key,
tbl_estoque int not null,

id_vendas int,
constraint fk_tbl_estoque_tbl_vendas
foreign key (id_vendas)
references sys_promocao.tbl_vendas(id_vendas),

id_Produto int,
constraint fk_tbl_estoque_tbl_produto
foreign key (id_produto)
references sys_promocao.tbl_produto(id_produto),

id_fornecedor int,
constraint fk_tbl_estoque_tbl_fornecedor
foreign key (id_produto)
references sys_promocao.tbl_fornecedor(id_fornecedor)
);

use sys_promocao;
select*from tbl_cliente;
show tables;
delete from tbl_compra
where id_compra = 3;

insert into tbl_cliente (nome_cliente,rg_cliente,data_nascimento,e_mail) 
value ('Leticia Aparecida','123453336','01-02-2020','leticia@gmail.com');

select*from tbl_produto;
insert into tbl_produto (nome_produto,quantidade_estoque,codigo,valor_compra,valor_venda,categoria) 
value ('chocolate Milka','1000','3','5','15','Doces');

select*from tbl_fornecedor;
insert into tbl_fornecedor (nome_fornecedor,nome_representante,logradouro,cep,bairro,cidade,estado,pais) 
value ('mondeles internacional','Evandro Castro','Av Luis Carlos Berrini','12343-210','Broklin','São Paulo','São Paulo','Brasil');   

select*from tbl_compra;
insert into tbl_compra (data_compras,total_compras,credito,pix,debito,dinheiro,id_cliente,id_Produto)
value ('1998-03-11',5,0,0,20,0,1,3);

select*from tbl_endereco;
insert into tbl_endereco (cep, logradouro, bairro, cidade, estado, pais, id_cliente)
value('22334-999', 'AV. Carlos Lacerda','Campo Limpo','Pelotas','Rio Grande do Sul','Brasil',5);

select * from tbl_vendas;
insert into tbl_vendas (total_de_vendas, data_vendas, total_credito, total_pix, total_debito, total_dinheiro, quantidade, preco, departamento, id_produto)
values(3,'2020-07-17',0,0,100,0,5,10,'bebida',1);

use sys_promocao;
select * from tbl_produto;
select * from tbl_vendas;
select * from tbl_cliente;
select * from tbl_colaborador;
select * from tbl_compra;

#Atualiza valores de uma tabela (não esquecer de colocar o critário de busca, pode ser o id)
update tbl_colaborador set nome = 'Ricardo Souza' 
where id_coladorador = 1;

#Ordenação de conteudo, crescente e decrescente, podendo ser por nome ou conteudo
select * from tbl_produto order by nome_produto asc;
select * from tbl_produto order by quantidade_estoque desc;
select * from tbl_produto order by quantidade_estoque asc;

#filtrando dados com critérios utilizando o peradores lógicos 
select * from tbl_produto where quantidade_estoque > 100;
select * from tbl_produto where quantidade_estoque <= 1000 and valor_compra > 2;

#filtrando dados com criterios utilizando operadores logicos (and, or,not)
select * from tbl_produto where quantidade_estoque <= 3000 and valor_compra < 50;

select * from tbl_produto where nome_produto = 'arroz';


select * from tbl_produto where nome_produto like 'arroz'; #igualdade
select * from tbl_produto where nome_produto like 'arroz%';# lista produtos que iniciam com a palavra
select * from tbl_produto where nome_produto like '%arroz';#lista produtos que terminam com a palavra
select * from tbl_produto where nome_produto like '%arroz%';# lista produtos que contenha a palavra em qualquer posição

SELECT tbl_cliente.nome_cliente, tbl_compra.data_compras, tbl_compra.total_compras, tbl_produto.nome_produto
FROM tbl_cliente
INNER JOIN tbl_compra
  ON tbl_cliente.id_cliente = tbl_compra.id_cliente
INNER JOIN tbl_produto
  ON tbl_compra.id_produto = tbl_produto.id_produto;
