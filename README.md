# AC2-Banco-de-Dados
Tema: Base de Dados Pizzaria (Modelo Lógico)

## Neste exercicio fizemos uma apresentação sobre um sistema de armazenamento de pizzas e funcionarios, incluindo os tipos de pizzas, ingredientes utilizados e qual funcionario faz determinada pizza

## modelo conceitual
### Um modelo conceitual é uma representação abstrata e simplificada de um sistema, processo, organização ou conceito.

#### 1-Transforme o modelo conceitual em modelo lógico
![diagrama modelo logico](https://github.com/GabrielChagasAlves/AC2-Banco-de-Dados/assets/125607847/8719ab8c-4dad-4615-a19e-6b6f9fce211a)

#### 2-Escreva o script SQL que cria o banco de dados 
```SQL
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`pizza`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`pizza` (
  `id_pizza` INT NOT NULL AUTO_INCREMENT,
  `Sabor` VARCHAR(2000) NULL,
  `Preco_pizza` DECIMAL(9,2) NULL,
  `Descricao` VARCHAR(2000) NULL,
  `Tamanho_pizza` CHAR(1) NULL,
  `Preco_embalagem` DECIMAL(9,2) NULL,
  `Tamanho_embalagem` CHAR(1) NULL,
  `Material` VARCHAR(2000) NULL,
  PRIMARY KEY (`id_pizza`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Receita`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Receita` (
  `id_Receita` INT NOT NULL AUTO_INCREMENT,
  `Instrucoes` VARCHAR(2000) NULL,
  `Autor` VARCHAR(2000) NULL,
  `pizza_id_pizza` INT NOT NULL,
  PRIMARY KEY (`id_Receita`, `pizza_id_pizza`),
  INDEX `fk_Receita_pizza1_idx` (`pizza_id_pizza` ASC) VISIBLE,
  CONSTRAINT `fk_Receita_pizza1`
    FOREIGN KEY (`pizza_id_pizza`)
    REFERENCES `mydb`.`pizza` (`id_pizza`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Pizzaiolo`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Pizzaiolo` (
  `id_Pizzaiolo` INT NOT NULL AUTO_INCREMENT,
  `Nome` VARCHAR(2000) NULL,
  `Salario` DECIMAL(9,2) NULL,
  PRIMARY KEY (`id_Pizzaiolo`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Ingredientes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Ingredientes` (
  `id_Ingredientes` INT NOT NULL AUTO_INCREMENT,
  `ingredientes_pizzas` VARCHAR(2000) NULL,
  PRIMARY KEY (`id_Ingredientes`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`pizza_has_Pizzaiolo`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`pizza_has_Pizzaiolo` (
  `pizza_id_pizza` INT NOT NULL,
  `Pizzaiolo_id_Pizzaiolo` INT NOT NULL,
  PRIMARY KEY (`pizza_id_pizza`, `Pizzaiolo_id_Pizzaiolo`),
  INDEX `fk_pizza_has_Pizzaiolo_Pizzaiolo1_idx` (`Pizzaiolo_id_Pizzaiolo` ASC) VISIBLE,
  INDEX `fk_pizza_has_Pizzaiolo_pizza1_idx` (`pizza_id_pizza` ASC) VISIBLE,
  CONSTRAINT `fk_pizza_has_Pizzaiolo_pizza1`
    FOREIGN KEY (`pizza_id_pizza`)
    REFERENCES `mydb`.`pizza` (`id_pizza`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_pizza_has_Pizzaiolo_Pizzaiolo1`
    FOREIGN KEY (`Pizzaiolo_id_Pizzaiolo`)
    REFERENCES `mydb`.`Pizzaiolo` (`id_Pizzaiolo`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`pizza_has_Ingredientes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`pizza_has_Ingredientes` (
  `pizza_id_pizza` INT NOT NULL,
  `Ingredientes_id_Ingredientes` INT NOT NULL,
  PRIMARY KEY (`pizza_id_pizza`, `Ingredientes_id_Ingredientes`),
  INDEX `fk_pizza_has_Ingredientes_Ingredientes1_idx` (`Ingredientes_id_Ingredientes` ASC) VISIBLE,
  INDEX `fk_pizza_has_Ingredientes_pizza1_idx` (`pizza_id_pizza` ASC) VISIBLE,
  CONSTRAINT `fk_pizza_has_Ingredientes_pizza1`
    FOREIGN KEY (`pizza_id_pizza`)
    REFERENCES `mydb`.`pizza` (`id_pizza`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_pizza_has_Ingredientes_Ingredientes1`
    FOREIGN KEY (`Ingredientes_id_Ingredientes`)
    REFERENCES `mydb`.`Ingredientes` (`id_Ingredientes`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

```
#### 3- Insira dados no banco criado
## Pizza
```SQL
-- Pizza 1
INSERT INTO pizza (Sabor, Preco_pizza, Descricao, Tamanho_pizza, Preco_embalagem, Tamanho_embalagem, Material)
VALUES ('Pizza Margherita', 12.99, 'Clássica pizza italiana com molho de tomate, queijo mozzarella e manjericão.', 'M', 0.5, 'P', 'Papelão');

-- Pizza 2
INSERT INTO pizza (Sabor, Preco_pizza, Descricao, Tamanho_pizza, Preco_embalagem, Tamanho_embalagem, Material)
VALUES ('Pizza Pepperoni', 14.99, 'Pizza com pepperoni, molho de tomate e queijo derretido.', 'G', 0.75, 'G', 'Papelão');

-- Pizza 3
INSERT INTO pizza (Sabor, Preco_pizza, Descricao, Tamanho_pizza, Preco_embalagem, Tamanho_embalagem, Material)
VALUES ('Pizza Vegetariana', 13.99, 'Pizza vegetariana com cogumelos, pimentões, cebola e azeitonas.', 'M', 0.5, 'M', 'Papelão');

-- Pizza 4
INSERT INTO pizza (Sabor, Preco_pizza, Descricao, Tamanho_pizza, Preco_embalagem, Tamanho_embalagem, Material)
VALUES ('Pizza Frango com Pesto', 15.99, 'Pizza com frango grelhado, molho pesto e tomate-cereja.', 'G', 0.75, 'G', 'Papelão');

-- Pizza 5
INSERT INTO pizza (Sabor, Preco_pizza, Descricao, Tamanho_pizza, Preco_embalagem, Tamanho_embalagem, Material)
VALUES ('Pizza Quatro Queijos', 14.49, 'Pizza com uma seleção de quatro queijos diferentes.', 'M', 0.5, 'P', 'Papelão');
```
## Ingredientes
```SQL 
INSERT INTO ingredientes (ingredientes_pizzas)
VALUES
  ('Molho de tomate'),
  ('Queijo mussarela'),
  ('Bacon'),
  ('Milho'),
  ('Pimenta calabresa'),
  ('Presunto'),
  ('Abacaxi'),
  ('Orégano'),
  ('Linguiça calabresa'),
  ('Cebola roxa'),
  ('Pimenta jalapeño'),
  ('Tomate em cubos'),
  ('Manjericão fresco'),
  ('Azeite de oliva extra virgem'),
  ('Cogumelos fatiados'),
  ('Azeitonas verdes'),
  ('Rúcula');
```
## Pizzaiolo
```SQL
INSERT INTO pizzaiolo (Nome, Salario) VALUES
('Toninho', 10000),
('Maria', 9500),
('Luigi', 11000),
('Isabela', 8800),
('Rafael', 10500);
```

## Receita-Cozinheiro
```SQL
INSERT INTO receita (Instrucoes, Autor, pizza_id_pizza) VALUES 
('Molho de tomate, Queijo mussarela, Bacon, Milho, Pimenta calabresa', 'Toninho', 1),
('Molho de tomate, Queijo mussarela, Presunto, Abacaxi, Orégano', 'Maria', 2),
('Molho de tomate, Queijo mussarela, Linguiça calabresa, Cebola roxa, Pimenta jalapeño', 'Luigi', 3),
('Molho de tomate, Queijo mussarela, Tomate em cubos, Manjericão fresco, Azeite de oliva extra virgem', 'Isabela', 4),
('Molho de tomate, Queijo mussarela, Cogumelos fatiados, Azeitonas verdes, Rúcula', 'Rafael', 5);
```
## Tabela de Relação Pizza-Pizzaiolo
```SQL
insert into pizza_has_pizzaiolo (pizza_id_pizza, pizzaiolo_id_Pizzaiolo)
values (1,1), (2,2), (3,3), (4,4), (5,5);
```
#### 4-Crie um relatório com todas as pizzas e os pizzaiolos aptos a produzi-las
```SQL
select pizza.Sabor as Saborpizza, pizzaiolo.Nome as pizzaiolo
from pizza
join pizza_has_pizzaiolo on pizza.id_pizza = pizza_has_pizzaiolo.pizza_id_pizza
join pizzaiolo on pizza_has_pizzaiolo.pizzaiolo_id_Pizzaiolo = pizzaiolo.id_Pizzaiolo;
```
![4](https://github.com/GabrielChagasAlves/AC2-Banco-de-Dados/assets/125607847/b882c184-c784-4b68-950c-4a0885257d46)

#### 5-Crie um relatório com todas as pizzas e seus ingredientes
```SQL
SELECT pizza.Sabor as Sabor,
GROUP_CONCAT(ingredientes.ingredientes_pizzas) as ingredientes
FROM pizza
JOIN pizza_has_ingredientes ON pizza.id_pizza = pizza_has_ingredientes.pizza_id_pizza
JOIN ingredientes ON pizza_has_ingredientes.Ingredientes_id_Ingredientes = Ingredientes.id_Ingredientes
GROUP BY pizza.Sabor;
```
![5](https://github.com/GabrielChagasAlves/AC2-Banco-de-Dados/assets/125607847/7b683702-561f-4f2b-9d91-9c4e810e89cc)


#### 6-Crie um relatório com todos os ingredientes e as pizzas onde são utilizados
```SQL
select 
	ingredientes.ingredientes_pizzas as Ingredientes,
    group_concat(pizza.sabor) as Sabor
from ingredientes join pizza_has_ingredientes on ingredientes.id_ingredientes =  pizza_has_ingredientes.ingredientes_id_ingredientes
join pizza on pizza_has_ingredientes.pizza_id_pizza = pizza.id_pizza
GROUP BY ingredientes.ingredientes_pizzas;
```
![6](https://github.com/GabrielChagasAlves/AC2-Banco-de-Dados/assets/125607847/37beeb53-0ea1-4f01-a6c8-f8240d3fe228)

#### 7-Crie um relatório com os sabores de todas as pizzas, o nome dos pizzaiolos que as fazem e as instruções para produzi-las.
```SQL
select 
	ingredientes.ingredientes_pizzas as Ingredientes,
    group_concat(pizza.sabor) as Sabor
from ingredientes join pizza_has_ingredientes on ingredientes.id_Ingredientes =  pizza_has_ingredientes.Ingredientes_id_Ingredientes
join pizza on pizza_has_ingredientes.pizza_id_pizza = pizza.id_pizza
GROUP BY ingredientes.ingredientes_pizzas;
```
![7](https://github.com/GabrielChagasAlves/AC2-Banco-de-Dados/assets/125607847/3d38fe1f-1711-43e9-94a4-88ef402a8f52)

