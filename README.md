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
