# Projeto de Banco de Dados para Loja de Produtos Tecnológicos

Este repositório contém o script SQL para a criação, atualização e gerenciamento de um banco de dados destinado a uma loja de produtos tecnológicos. O objetivo principal é melhorar a organização e a consulta de produtos, proporcionando um sistema mais eficiente e funcional para o cliente.

## Funcionalidades Implementadas

1. **Criação do Banco de Dados e Tabela Inicial**
    ```sql
    CREATE DATABASE Loja;
    USE Loja;
    CREATE TABLE Produtos (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nome VARCHAR(255) NOT NULL
    );
    ```

2. **Inserção de Dados Iniciais**
    ```sql
    INSERT INTO Produtos (nome) VALUES 
    ('Processador Intel i7'),
    ('Placa de Vídeo NVIDIA GTX 1080'),
    ('Placa Mãe ASUS'),
    ('Memória RAM 16GB DDR4'),
    ('SSD 1TB Samsung');
    ```

3. **Alteração da Tabela Produtos**
    ```sql
    ALTER TABLE Produtos ADD categoria VARCHAR(255);
    ALTER TABLE Produtos ADD valor DECIMAL(10, 2);
    ALTER TABLE Produtos ADD cor VARCHAR(50);
    ```

4. **Atualização dos Dados**
    ```sql
    UPDATE Produtos SET categoria = 'Processador', valor = 1200.00, cor = 'Cinza' WHERE nome = 'Processador Intel i7';
    UPDATE Produtos SET categoria = 'Placa de Vídeo', valor = 2500.00, cor = 'Preto' WHERE nome = 'Placa de Vídeo NVIDIA GTX 1080';
    UPDATE Produtos SET categoria = 'Placa Mãe', valor = 800.00, cor = 'Preto' WHERE nome = 'Placa Mãe ASUS';
    UPDATE Produtos SET categoria = 'Memória RAM', valor = 600.00, cor = 'Verde' WHERE nome = 'Memória RAM 16GB DDR4';
    UPDATE Produtos SET categoria = 'SSD', valor = 700.00, cor = 'Preto' WHERE nome = 'SSD 1TB Samsung';
    ```

5. **Criação de Tabelas Relacionadas**
    ```sql
    CREATE TABLE Fornecedores (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nome VARCHAR(255) NOT NULL
    );

    CREATE TABLE ProdutoFornecedores (
        id INT AUTO_INCREMENT PRIMARY KEY,
        produto_id INT,
        fornecedor_id INT,
        FOREIGN KEY (produto_id) REFERENCES Produtos(id),
        FOREIGN KEY (fornecedor_id) REFERENCES Fornecedores(id)
    );
    ```

6. **Inserção de Dados nas Tabelas Relacionadas**
    ```sql
    INSERT INTO Fornecedores (nome) VALUES ('Fornecedor A'), ('Fornecedor B');

    INSERT INTO ProdutoFornecedores (produto_id, fornecedor_id) VALUES 
    (1, 1),
    (2, 1),
    (3, 2),
    (4, 2),
    (5, 1);
    ```

7. **Consultas SQL Avançadas**
    ```sql
    -- INNER JOIN
    SELECT p.nome AS produto, f.nome AS fornecedor
    FROM Produtos p
    INNER JOIN ProdutoFornecedores pf ON p.id = pf.produto_id
    INNER JOIN Fornecedores f ON pf.fornecedor_id = f.id;

    -- LEFT JOIN
    SELECT p.nome AS produto, f.nome AS fornecedor
    FROM Produtos p
    LEFT JOIN ProdutoFornecedores pf ON p.id = pf.produto_id
    LEFT JOIN Fornecedores f ON pf.fornecedor_id = f.id;
    ```

    ```sql
    -- Subconsulta com IN
    SELECT nome FROM Produtos
    WHERE id IN (SELECT produto_id FROM ProdutoFornecedores WHERE fornecedor_id = 1);

    -- Subconsulta com NOT IN
    SELECT nome FROM Produtos
    WHERE id NOT IN (SELECT produto_id FROM ProdutoFornecedores);

    -- Subconsulta com EXISTS
    SELECT nome FROM Produtos p
    WHERE EXISTS (SELECT 1 FROM ProdutoFornecedores pf WHERE pf.produto_id = p.id AND pf.fornecedor_id = 2);
    ```

8. **Consultas Simples**
    ```sql
    -- Select simples 1
    SELECT * FROM Produtos;

    -- Select simples 2
    SELECT nome, valor FROM Produtos WHERE valor > 1000;
    ```

## Como Usar

1. Clone este repositório:
    ```sh
    git clone https://github.com/seu-usuario/nome-do-repositorio.git
    ```

2. Importe o arquivo `.sql` para seu banco de dados MySQL:
    ```sh
    mysql -u seu-usuario -p sua-senha Loja < caminho/do/arquivo.sql
    ```

3. Execute as consultas SQL fornecidas para interagir e testar as funcionalidades do banco de dados.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues e pull requests para melhorias e correções.

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).

