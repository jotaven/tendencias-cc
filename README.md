# Relatório de Exercícios: Bancos de Dados NoSQL e Vetoriais

### 1) Criação do Keyspace

### Comando

`CREATE KEYSPACE ecommerce
WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};`

### 2) Selecionar o Keyspace

### Comando

Snippet de código

`USE ecommerce;`

### 3) Criação de Tabela de Clientes

### Comando

`CREATE TABLE clientes ( id_cliente UUID PRIMARY KEY, nome TEXT,
email TEXT, pais TEXT
);`

### Resultado

### 4) Inserção de Registros

### Comando

Snippet de código

`INSERT INTO clientes (id_cliente, nome, email, pais)
VALUES (uuid(), 'Maria Lima', 'maria.lima@gmail.com', 'Brasil');

INSERT INTO clientes (id_cliente, nome, email, pais)
VALUES (uuid(), 'John Smith', 'john.smith@yahoo.com', 'EUA');

INSERT INTO clientes (id_cliente, nome, email, pais)
VALUES (uuid(), 'Ana Torres', 'ana.torres@outlook.com', 'Portugal');`

### 5) Consulta Simples

### Comando

Snippet de código

`SELECT * FROM clientes;`

### Resultado

![Captura de Tela 2025-11-13 às 00.42.22.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.42.22.png)

### 6) Filtragem com ALLOW FILTERING

### Comando

Snippet de código

`SELECT nome, email FROM clientes WHERE pais = 'Brasil' ALLOW FILTERING;`

### Resultado

![Captura de Tela 2025-11-13 às 00.43.46.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.43.46.png)

### 7) Atualização de Dados

### Comando

Snippet de código

`UPDATE clientes
SET email = 'maria.lima@empresa.com.br'
WHERE id_cliente = c8033726-3202-4867-a025-272565e7d421;`

### 8) Criação de Índice Secundário

### Comando

Snippet de código

`CREATE INDEX idx_pais ON clientes (pais);`

### 9) Criação de Outra Tabela e Junção Lógica

### Comando

Snippet de código

`CREATE TABLE pedidos ( id_pedido UUID PRIMARY KEY, id_cliente UUID,
data_pedido DATE, valor_total DECIMAL
);

INSERT INTO pedidos (id_pedido, id_cliente, data_pedido, valor_total) VALUES (uuid(),
'c8033726-3202-4867-a025-272565e7d421', '2024-09-01', 299.90);`

### 10) Exclusão e Limpeza de Dados

### Comando

Snippet de código

`TRUNCATE clientes;`

### Resultado

### Desafio Extra – Replicação em Múltiplos Datacenters

### Comando

Snippet de código

`CREATE KEYSPACE global_store
WITH replication = {
'class': 'NetworkTopologyStrategy', 'us_east': 2,
'eu_west': 2
};`

---

## 2. Lista de Exercícios – Neo4j (Cypher)

### 1) Criando Nós Simples

### Comando

Cypher

`CREATE (a:Pessoa {nome:'Alice', idade:25}), (b:Pessoa {nome:'Bruno', idade:30}),
(c:Pessoa {nome:'Carla', idade:28});`

### Resultado

![Captura de Tela 2025-11-13 às 00.48.26.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.48.26.png)

### 2) Criando Relacionamentos

### Comando

Cypher

`MATCH (a:Pessoa {nome:'Alice'}), (b:Pessoa {nome:'Bruno'}) CREATE (a)-
[:AMIGO_DE]->(b);`

### Resultado

![Captura de Tela 2025-11-13 às 00.48.42.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.48.42.png)

### 3) Consultando Nós e Relações

### Comando

Cypher

`MATCH (p1:Pessoa)-[:AMIGO_DE]->(p2:Pessoa) RETURN p1.nome, 'é amigo de',
p2.nome;`

### Resultado

![Captura de Tela 2025-11-13 às 00.48.55.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.48.55.png)

### 4) Filtrando Dados

### Comando

Cypher

`MATCH (p:Pessoa) WHERE p.idade > 26 RETURN p.nome, p.idade;`

![Captura de Tela 2025-11-13 às 00.49.27.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.49.27.png)

### Resultado

### 5) Atualizando Propriedades

### Comando

Cypher

`MATCH (p:Pessoa {nome:'Bruno'}) SET p.idade = 31;`

### Resultado

![Captura de Tela 2025-11-13 às 00.49.41.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.49.41.png)

### 6) Excluindo Nós e Relacionamentos

### Comando

Cypher

`MATCH (a:Pessoa {nome:'Alice'})-[r:AMIGO_DE]->(b:Pessoa
{nome:'Bruno'}) DELETE r;`

### Resultado

![Captura de Tela 2025-11-13 às 00.49.56.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.49.56.png)

### 7) Criando um Grafo de Filmes

### Comando

Cypher

`CREATE (m:Filme {titulo:'Matrix', ano:1999}), (a:Ator {nome:'Keanu Reeves'}),
(a)-[:ATUOU_EM]->(m);`

### Resultado

![Captura de Tela 2025-11-13 às 00.50.09.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.50.09.png)

### 8) Consultas com Caminhos

### Comando

Cypher

`MATCH (a:Ator {nome:'Keanu Reeves'})-[:ATUOU_EM]->(m:Filme) RETURN a.nome, 
m.titulo, m.ano;`

### Resultado

![Captura de Tela 2025-11-13 às 00.50.26.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.50.26.png)

### 9) Funções de Agregação

### Comando

Cypher

`MATCH (a:Ator)-[:ATUOU_EM]->(m:Filme)
RETURN a.nome, COUNT(m) AS total_filmes;`

### Resultado

![Captura de Tela 2025-11-13 às 00.50.43.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.50.43.png)

### 10) Índices e Constraints

### Comando

Cypher

`CREATE INDEX ator_nome_index FOR (a:Ator) ON (a.nome);`

### Resultado

![Captura de Tela 2025-11-13 às 00.50.59.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.50.59.png)

### 11) Caminhos Mais Curtos

### Comando

Cypher

`MATCH p = shortestPath((a:Pessoa {nome:'Alice'})-[:AMIGO_DE*]- (b:Pessoa
{nome:'Carla'}))
RETURN p;`

### Resultado

![Captura de Tela 2025-11-13 às 00.51.10.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.51.10.png)

### 12) Consultas com Coleta

### Comando

Cypher

`MATCH (a:Ator)-[:ATUOU_EM]->(m:Filme)
RETURN m.ano, COLLECT(a.nome) AS elenco, COUNT(a) AS total_atores;`

### Resultado

![Captura de Tela 2025-11-13 às 00.51.23.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.51.23.png)

### Desafio Final – Sistema de Recomendação

### Comando

Cypher

`MATCH (p1:Pessoa)-[r1:ASSISTIU]->(f:Filme)<-[r2:ASSISTIU]-
(p2:Pessoa)
WHERE p1 <> p2 AND abs(r1.nota - r2.nota) < 1
RETURN DISTINCT f.titulo AS recomendacao, p2.nome AS origem LIMIT 10;`

### Resultado

![Captura de Tela 2025-11-13 às 00.51.39.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.51.39.png)

### Dica Extra: Visualização do Schema

### Comando

Cypher

`CALL db.schema.visualization();`

### Resultado

![Captura de Tela 2025-11-13 às 00.52.03.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.52.03.png)

---

## 3. Lista de Exercícios — Banco de Dados Vetorial com pgvector

### 1) Instalação da Extensão

### Comando

SQL

`CREATE EXTENSION IF NOT EXISTS vector;`

### Resultado

![Captura de Tela 2025-11-13 às 00.55.59.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.55.59.png)

### 2) Verificação da Extensão

### Comando

SQL

`\dx`

### Resultado

![Captura de Tela 2025-11-13 às 00.55.27.png](Relat%C3%B3rio%20de%20Exerc%C3%ADcios%20Bancos%20de%20Dados%20NoSQL%20e%20Ve/Captura_de_Tela_2025-11-13_as_00.55.27.png)

### 3) Criação de Tabela Vetorial

### Comando

SQL

`CREATE TABLE documentos (` 

`id SERIAL PRIMARY KEY,`

`id BIGSERIAL PRIMARY KEY, 
titulo TEXT,
conteudo TEXT, embedding VECTOR(3)
);`

### Resultado

### 4) Inserção de Vetores

SQL

`INSERT INTO documentos (titulo, conteudo, embedding) VALUES
('Doc 1', 'Introdução à IA', '[0.8, 0.1, 0.3]'::vector),
('Doc 2', 'Técnicas de ML', '[0.7, 0.2, 0.4]'::vector),
('Doc 3', 'Redes Neurais', '[0.4, 0.9, 0.1]'::vector),
('Doc 4', 'Visão Computacional', '[0.83, 0.05, 0.27]'::vector),
('Doc 5', 'Processamento de Linguagem Natural', '[0.6, 0.15, 0.35]'::vector);`

### Resultado

### 5) Similaridade Cosseno (Top 3)

SQL

`SELECT id, titulo, 1 - (embedding <=> '[0.8,0.1,0.3]'::vector) AS cosine_similarity
FROM documentos
ORDER BY embedding <=> '[0.8,0.1,0.3]'::vector LIMIT 3;`

### 6) Distância Euclidiana (L2)

SQL

`SELECT id, titulo, embedding <-> '[0.8,0.1,0.3]'::vector AS l2_distance
FROM documentos
ORDER BY embedding <-> '[0.8,0.1,0.3]'::vector LIMIT 3;`

### 7) Inner Product

### Comando

SQL

`SELECT id, titulo, (embedding <#> '[0.8,0.1,0.3]'::vector) AS neg_inner_product
FROM documentos
ORDER BY embedding <#> '[0.8,0.1,0.3]'::vector LIMIT 3;`

### 8) Índice IVFFLAT

### Comando

SQL

`CREATE INDEX ON documentos USING ivfflat (embedding vector_cosine_ops) WITH (lists = 100);`

### 9) Ajuste de Parâmetros (lists = 100)

### Comando

SQL

`DROP INDEX IF EXISTS documentos_embedding_ivfflat_idx; 
CREATE INDEX documentos_embedding_ivfflat_idx ON documentos USING ivfflat (embedding
vector_cosine_ops) WITH (lists = 100);`

### 10) Verificar uso de índice (EXPLAIN ANALYZE)

### Comando

SQL

`EXPLAIN ANALYZE
SELECT id, titulo FROM documentos
ORDER BY embedding <=> '[0.8,0.1,0.3]'::vector LIMIT 3;`

### 11) pg_trgm e tsvector

### Comando

SQL

`CREATE EXTENSION IF NOT EXISTS pg_trgm;
ALTER TABLE documentos ADD COLUMN conteudo_tsv tsvector; 
UPDATE documentos SET conteudo_tsv = to_tsvector('portuguese', conteudo);
CREATE INDEX idx_documentos_conteudo_tsv ON documentos USING GIN
(conteudo_tsv);`

### 12) Consulta BM25 (texto)

### Comando

SQL

`SELECT id, titulo, ts_rank_cd(conteudo_tsv, plainto_tsquery('portuguese', 'inteligência'))
AS rank
FROM documentos
WHERE conteudo_tsv @@ plainto_tsquery('portuguese', 'inteligência') ORDER BY rank
DESC
LIMIT 5;`

### 13) Combinação Híbrida (vetor + BM25)

### Comando

SQL

`SELECT d.id, d.titulo,
(0.7 * (1 - (d.embedding <=> q)) + 0.3 * (bm25_rank / greatest_bm25)) AS hybrid_score
FROM documentos d,
(SELECT '[0.8,0.1,0.3]'::vector AS q) AS sub,
(SELECT MAX(ts_rank_cd(conteudo_tsv, plainto_tsquery('portuguese','inteligência')))
AS greatest_bm25 FROM documentos) AS bm
ORDER BY hybrid_score DESC LIMIT 5;`

### 14) Inserção em Massa (simular 100 embeddings)

### Comando

SQL

`INSERT INTO documentos (titulo, conteudo, embedding) SELECT
'Doc_sim_' || i, 'Conteúdo simulado ' || i,
(ARRAY[random(), random(), random()])::vector FROM generate_series(1,100) AS s(i);`

### 15) Normalização de Vetores (coluna calculada)

### Comando

SQL

`ALTER TABLE documentos ADD COLUMN embedding_norm VECTOR(3);
UPDATE documentos SET embedding_norm = (embedding / sqrt( (embedding <#>
embedding) * -1 ));`

### 16) Trigger para atualizar normalização automaticamente

### Comando

SQL

`CREATE OR REPLACE FUNCTION update_embedding_norm() RETURNS trigger AS
$$
BEGIN
NEW.embedding_norm := NEW.embedding / sqrt( (NEW.embedding <#>
NEW.embedding) * -1 ); -- conceitual
RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_norm BEFORE INSERT OR UPDATE ON
documentos
FOR EACH ROW EXECUTE FUNCTION update_embedding_norm();`

### 17) Armazenamento em JSONB

### Comando

SQL

`ALTER TABLE documentos ADD COLUMN metadados JSONB;
UPDATE documentos SET metadados = '{"autor":"Maria","data":"2025-11-
01","categoria":"IA"}' WHERE id = 1;`

### 18) Consulta por Metadados + Similaridade

### Comando

SQL

`SELECT d.id, d.titulo, 1 - (d.embedding <=> '[0.8,0.1,0.3]'::vector) AS cosine_similarity
FROM documentos d
WHERE d.metadados ->> 'categoria' = 'IA'
AND (1 - (d.embedding <=> '[0.8,0.1,0.3]'::vector)) > 0.8 ORDER BY cosine_similarity
DESC;`

### 19) Média das Distâncias Cosseno

### Comando

SQL

`WITH pairs AS (
SELECT a.id AS ida, b.id AS idb, (a.embedding <=> b.embedding) AS cosine_distance
FROM documentos a
JOIN documentos b ON a.id < b.id
)
SELECT AVG(cosine_distance) AS avg_cosine_distance FROM pairs;`

### 20) View Top-3 Similares (vw_top_similares)

SQL

`CREATE VIEW vw_top_similares AS
SELECT d.id AS doc_id, d.titulo AS doc_titulo, s.similar_id, s.similar_title,
s.cosine_similarity
FROM documentos d, LATERAL (
SELECT id AS similar_id, titulo AS similar_title, 1 - (embedding <=> d.embedding) AS
cosine_similarity
FROM documentos WHERE id != d.id
ORDER BY embedding <=> d.embedding LIMIT 3
) s;`