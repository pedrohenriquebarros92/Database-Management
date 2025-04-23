-- -----------------------------------------------------
-- SCRIPT COMPLETO - ESCOLA DE MÚSICA
-- Modelagem MR + Scripts DDL, DML, DQL
-- -----------------------------------------------------

-- ======================================
-- 1. CRIAÇÃO DAS TABELAS (DDL)
-- ======================================
CREATE TABLE Orquestra (
    id_orquestra INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    cidade VARCHAR(100),
    pais VARCHAR(100),
    data_criacao DATE
);

CREATE TABLE Sinfonia (
    id_sinfonia INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    compositor VARCHAR(100),
    data_criacao DATE,
    duracao INT
);

CREATE TABLE Musico (
    id_musico INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    identidade VARCHAR(100),
    nacionalidade VARCHAR(50),
    data_nascimento DATE,
    email VARCHAR(100),
    id_orquestra INT,
    FOREIGN KEY (id_orquestra) REFERENCES Orquestra(id_orquestra),
    CONSTRAINT chk_data_nascimento CHECK (data_nascimento < CURDATE())
);

CREATE TABLE Funcao_Sinfonia (
    id_funcao INT AUTO_INCREMENT PRIMARY KEY,
    id_musico INT,
    id_sinfonia INT,
    funcao VARCHAR(50),
    instrumento VARCHAR(50),
    data_assumiu DATE,
    local_apresentacao VARCHAR(100),
    FOREIGN KEY (id_musico) REFERENCES Musico(id_musico),
    FOREIGN KEY (id_sinfonia) REFERENCES Sinfonia(id_sinfonia),
    CONSTRAINT chk_data_assumiu CHECK (data_assumiu < CURDATE())
);

CREATE TABLE Instrumento (
    id_instrumento INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50),
    tipo VARCHAR(50)
);

CREATE TABLE Musico_Instrumento (
    id_musico INT,
    id_instrumento INT,
    PRIMARY KEY (id_musico, id_instrumento),
    FOREIGN KEY (id_musico) REFERENCES Musico(id_musico),
    FOREIGN KEY (id_instrumento) REFERENCES Instrumento(id_instrumento)
);

-- ======================================
-- 2. VIEWS INICIAIS
-- ======================================
CREATE VIEW v_musicos_orquestra AS
SELECT m.nome AS musico, o.nome AS orquestra
FROM Musico m
JOIN Orquestra o ON m.id_orquestra = o.id_orquestra;

CREATE VIEW v_funcoes_musicais AS
SELECT m.nome AS musico, s.nome AS sinfonia, f.funcao, f.instrumento
FROM Funcao_Sinfonia f
JOIN Musico m ON f.id_musico = m.id_musico
JOIN Sinfonia s ON f.id_sinfonia = s.id_sinfonia;

-- ======================================
-- 3. ALTERAÇÕES NAS TABELAS (DDL)
-- ======================================
ALTER TABLE Orquestra ADD COLUMN descricao TEXT;
ALTER TABLE Musico ADD COLUMN email VARCHAR(100);
ALTER TABLE Musico MODIFY identidade VARCHAR(100);
ALTER TABLE Instrumento ADD COLUMN tipo VARCHAR(50);
ALTER TABLE Sinfonia ADD COLUMN duracao INT;
ALTER TABLE Funcao_Sinfonia ADD COLUMN local_apresentacao VARCHAR(100);
ALTER TABLE Orquestra ADD UNIQUE(nome);
ALTER TABLE Sinfonia ADD INDEX(nome);
ALTER TABLE Musico ADD CONSTRAINT chk_data_nascimento CHECK (data_nascimento < CURDATE());
ALTER TABLE Funcao_Sinfonia ADD CONSTRAINT chk_data_assumiu CHECK (data_assumiu < CURDATE());

-- ======================================
-- 4. DESTRUIÇÃO DO BANCO DE DADOS (DDL)
-- ======================================
DROP VIEW IF EXISTS v_musicos_orquestra;
DROP VIEW IF EXISTS v_funcoes_musicais;
DROP TABLE IF EXISTS Musico_Instrumento;
DROP TABLE IF EXISTS Funcao_Sinfonia;
DROP TABLE IF EXISTS Musico;
DROP TABLE IF EXISTS Sinfonia;
DROP TABLE IF EXISTS Instrumento;
DROP TABLE IF EXISTS Orquestra;

-- ======================================
-- 5. POPULANDO TABELAS (DML)
-- ======================================
INSERT INTO Instrumento (nome, tipo) VALUES
('Violino', 'Cordas'), ('Flauta', 'Sopro'), ('Trompete', 'Metais'),
('Piano', 'Teclas'), ('Violoncelo', 'Cordas'), ('Oboé', 'Sopro'),
('Contrabaixo', 'Cordas'), ('Tímpano', 'Percussão'), ('Clarinete', 'Sopro'), ('Harpa', 'Cordas');

INSERT INTO Orquestra (nome, cidade, pais, data_criacao) VALUES
('Filarmônica Brasileira', 'São Paulo', 'Brasil', '1985-04-10'),
('Orquestra Sinfônica Jovem', 'Rio de Janeiro', 'Brasil', '1990-03-12'),
('Orquestra Municipal de Belo Horizonte', 'Belo Horizonte', 'Brasil', '1975-01-01'),
('Sinfônica de Viena', 'Viena', 'Áustria', '1900-10-15'),
('London Symphony Orchestra', 'Londres', 'Reino Unido', '1904-06-14'),
('Orquestra de Paris', 'Paris', 'França', '1967-09-30'),
('Filarmônica de Berlim', 'Berlim', 'Alemanha', '1882-02-19'),
('Orquestra de Roma', 'Roma', 'Itália', '1940-11-22'),
('Sinfônica de Tóquio', 'Tóquio', 'Japão', '1950-05-05'),
('Orquestra Nacional da China', 'Pequim', 'China', '1960-08-08');

INSERT INTO Sinfonia (nome, compositor, data_criacao, duracao) VALUES
('Sinfonia Nº 5', 'Beethoven', '1808-12-22', 33),
('Sinfonia Nº 9', 'Beethoven', '1824-05-07', 70),
('Sinfonia do Novo Mundo', 'Dvořák', '1893-12-15', 40),
('Sinfonia Pastoral', 'Beethoven', '1808-12-22', 42),
('Sinfonia Nº 40', 'Mozart', '1788-07-25', 35),
('Sinfonia Nº 94', 'Haydn', '1791-03-23', 30),
('Sinfonia Nº 41', 'Mozart', '1788-08-10', 39),
('Sinfonia Italiana', 'Mendelssohn', '1833-05-13', 34),
('Sinfonia Fantástica', 'Berlioz', '1830-12-05', 45),
('Sinfonia Alpina', 'Richard Strauss', '1915-10-28', 50);

INSERT INTO Musico (nome, identidade, nacionalidade, data_nascimento, email, id_orquestra) VALUES
('Carlos Silva', 'ID001', 'Brasileira', '1980-06-10', 'carlos@email.com', 1),
('Ana Paula', 'ID002', 'Brasileira', '1990-07-15', 'ana@email.com', 1),
('João Mendes', 'ID003', 'Brasileira', '1985-04-20', 'joao@email.com', 2),
('Julia Santos', 'ID004', 'Brasileira', '1992-10-11', 'julia@email.com', 2),
('Luiz Fernando', 'ID005', 'Alemã', '1975-03-03', 'luiz@email.com', 3),
('Karin Müller', 'ID006', 'Alemã', '1988-05-19', 'karin@email.com', 3),
('Hiroshi Yamato', 'ID007', 'Japonesa', '1991-11-29', 'hiroshi@email.com', 4),
('Marie Dupont', 'ID008', 'Francesa', '1983-02-25', 'marie@email.com', 5),
('Luca Romano', 'ID009', 'Italiana', '1986-08-17', 'luca@email.com', 6),
('Sofia Oliveira', 'ID010', 'Brasileira', '1994-09-23', 'sofia@email.com', 1);

-- Associação entre músicos e instrumentos
INSERT INTO Musico_Instrumento (id_musico, id_instrumento) VALUES
(1, 1), (1, 2), (2, 5), (3, 3), (4, 4), (5, 6), (6, 7), (7, 8), (8, 9), (9, 10);

-- Funções nas sinfonias
INSERT INTO Funcao_Sinfonia (id_musico, id_sinfonia, funcao, instrumento, data_assumiu, local_apresentacao) VALUES
(1, 1, 'Violinista', 'Violino', '2020-01-10', 'Teatro Municipal'),
(2, 1, 'Violoncelista', 'Violoncelo', '2020-01-10', 'Teatro Municipal'),
(3, 2, 'Pianista', 'Piano', '2021-02-14', 'Sala São Paulo'),
(4, 3, 'Flautista', 'Flauta', '2019-03-12', 'Auditório Ibirapuera'),
(5, 4, 'Maestro', 'N/A', '2018-04-20', 'Berlim Philharmonie'),
(6, 5, 'Clarinetista', 'Clarinete', '2017-05-25', 'Paris Philharmonie'),
(7, 6, 'Percussionista', 'Tímpano', '2022-06-30', 'Tokyo Opera City'),
(8, 7, 'Oboísta', 'Oboé', '2020-07-07', 'Champs Elysées'),
(9, 8, 'Harpista', 'Harpa', '2023-08-08', 'Coliseu de Roma'),
(10, 9, 'Contrabaixista', 'Contrabaixo', '2023-09-01', 'Teatro Amazonas');

-- ======================================
-- 6. ATUALIZAÇÕES E DELETES (DML)
-- ======================================
UPDATE Musico SET nome = 'Carlos Eduardo Silva' WHERE id_musico = 1;
UPDATE Instrumento SET tipo = 'Sopro-Metal' WHERE nome = 'Trompete';
UPDATE Sinfonia SET duracao = 75 WHERE nome = 'Sinfonia Nº 9';
UPDATE Musico SET email = 'sofia.oliveira@email.com' WHERE id_musico = 10;
UPDATE Funcao_Sinfonia SET local_apresentacao = 'Sala São Paulo' WHERE id_funcao = 3;
UPDATE Orquestra SET cidade = 'São Paulo - SP' WHERE id_orquestra = 1;
DELETE FROM Funcao_Sinfonia WHERE id_funcao = 10;
DELETE FROM Musico_Instrumento WHERE id_musico = 6 AND id_instrumento = 7;
DELETE FROM Instrumento WHERE nome = 'Tímpano';
DELETE FROM Musico WHERE id_musico = 9;

-- ======================================
-- 7. RELATÓRIOS / CONSULTAS IMPORTANTES (DQL)
-- ======================================
-- 1
SELECT m.nome, o.nome FROM Musico m JOIN Orquestra o ON m.id_orquestra = o.id_orquestra;
-- 2
SELECT s.nome, f.funcao, COUNT(*) FROM Funcao_Sinfonia f JOIN Sinfonia s ON f.id_sinfonia = s.id_sinfonia GROUP BY s.nome, f.funcao;
-- 3
SELECT m.nome FROM Musico m JOIN Musico_Instrumento mi ON m.id_musico = mi.id_musico JOIN Instrumento i ON mi.id_instrumento = i.id_instrumento WHERE i.nome = 'Violino';
-- 4
SELECT s.nome, s.compositor, COUNT(f.id_musico) AS num_musicos FROM Sinfonia s JOIN Funcao_Sinfonia f ON s.id_sinfonia = f.id_sinfonia GROUP BY s.nome, s.compositor;
-- 5
SELECT m.nome, f.funcao FROM Musico m JOIN Funcao_Sinfonia f ON m.id_musico = f.id_musico WHERE f.instrumento = 'Flauta';
-- 6
SELECT o.nome, COUNT(m.id_musico) FROM Orquestra o JOIN Musico m ON o.id_orquestra = m.id_orquestra GROUP BY o.nome;
-- 7
SELECT nome FROM Sinfonia WHERE duracao > 40;
-- 8
SELECT m.nome, i.nome FROM Musico m JOIN Musico_Instrumento mi ON m.id_musico = mi.id_musico JOIN Instrumento i ON mi.id_instrumento = i.id_instrumento;
-- 9
SELECT DISTINCT f.funcao FROM Funcao_Sinfonia f;
-- 10
SELECT m.nome FROM Musico m WHERE m.data_nascimento < '1990-01-01';
-- 11
SELECT s.nome FROM Sinfonia s WHERE s.compositor LIKE '%Mozart%';
-- 12
SELECT i.nome, COUNT(*) FROM Musico_Instrumento mi JOIN Instrumento i ON mi.id_instrumento = i.id_instrumento GROUP BY i.nome;
-- 13
SELECT m.nome, f.data_assumiu FROM Musico m JOIN Funcao_Sinfonia f ON m.id_musico = f.id_musico WHERE f.funcao = 'Maestro';
-- 14
SELECT nome FROM Orquestra ORDER BY data_criacao ASC;
-- 15
SELECT s.nome, f.local_apresentacao FROM Funcao_Sinfonia f JOIN Sinfonia s ON f.id_sinfonia = s.id_sinfonia;
-- 16
SELECT m.nome, COUNT(f.id_sinfonia) FROM Musico m JOIN Funcao_Sinfonia f ON m.id_musico = f.id_musico GROUP BY m.nome;
-- 17
SELECT i.tipo, COUNT(*) FROM Instrumento i GROUP BY i.tipo;
-- 18
SELECT * FROM Musico WHERE email LIKE '%email.com';
-- 19
SELECT o.nome, o.cidade, o.pais FROM Orquestra o WHERE o.pais = 'Brasil';
-- 20
SELECT s.nome, COUNT(f.id_musico) AS qtd_musicos FROM Funcao_Sinfonia f JOIN Sinfonia s ON s.id_sinfonia = f.id_sinfonia GROUP BY s.nome;

-- ======================================
-- 8. CRIAÇÃO DE VIEWS PARA RELATÓRIOS (DDL)
-- ======================================
CREATE VIEW v_musicos_com_instrumentos AS
SELECT m.nome, i.nome AS instrumento FROM Musico m
JOIN Musico_Instrumento mi ON m.id_musico = mi.id_musico
JOIN Instrumento i ON mi.id_instrumento = i.id_instrumento;

CREATE VIEW v_sinfonias_com_maestro AS
SELECT s.nome AS sinfonia, m.nome AS maestro
FROM Funcao_Sinfonia f
JOIN Musico m ON f.id_musico = m.id_musico
JOIN Sinfonia s ON f.id_sinfonia = s.id_sinfonia
WHERE f.funcao = 'Maestro';

CREATE VIEW v_orquestras_brasileiras AS
SELECT * FROM Orquestra WHERE pais = 'Brasil';

CREATE VIEW v_instr_por_tipo AS
SELECT tipo, COUNT(*) AS total FROM Instrumento GROUP BY tipo;

CREATE VIEW v_idade_musicos AS
SELECT nome, YEAR(CURDATE()) - YEAR(data_nascimento) AS idade FROM Musico;

CREATE VIEW v_musicos_maiores_30 AS
SELECT * FROM v_idade_musicos WHERE idade > 30;

CREATE VIEW v_musicos_funcoes AS
SELECT m.nome, f.funcao, s.nome AS sinfonia FROM Musico m
JOIN Funcao_Sinfonia f ON m.id_musico = f.id_musico
JOIN Sinfonia s ON f.id_sinfonia = s.id_sinfonia;

CREATE VIEW v_sinfonia_participacao AS
SELECT s.nome, COUNT(f.id_musico) AS participantes FROM Sinfonia s
JOIN Funcao_Sinfonia f ON s.id_sinfonia = f.id_sinfonia
GROUP BY s.nome;

CREATE VIEW v_musico_email_contato AS
SELECT nome, email FROM Musico;

CREATE VIEW v_musico_orquestra_email AS
SELECT m.nome, o.nome AS orquestra, m.email FROM Musico m
JOIN Orquestra o ON m.id_orquestra = o.id_orquestra;

-- FIM DO SCRIPT
