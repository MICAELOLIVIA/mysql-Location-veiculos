# 🚗 CARPLACE | Banco de Dados MySQL

Projeto de estudo desenvolvido em **MySQL** para representar parte do banco de dados de uma concessionária de veículos. O objetivo é praticar a criação de tabelas, a organização de registros e o relacionamento entre entidades usando SQL.

## 📌 Sobre o projeto

O banco de dados `carplace` contém informações sobre **clientes**, **marcas de automóveis** e **veículos disponíveis no inventário**. É um projeto introdutório, criado para exercitar conceitos fundamentais de bancos de dados relacionais.

## 🛠️ Tecnologias

- MySQL 8.0
- MySQL Workbench (exportação do banco)
- SQL

## 🗂️ Estrutura do banco

### `clientes`
| Coluna | Tipo | Descrição |
|---|---|---|
| `id` | INT | Identificador único (chave primária) |
| `nome` | VARCHAR(250) | Nome do cliente |
| `sobrenome` | VARCHAR(250) | Sobrenome do cliente |
| `endereco` | VARCHAR(250) | Endereço do cliente |

### `marcas`
| Coluna | Tipo | Descrição |
|---|---|---|
| `id` | INT | Identificador único (chave primária) |
| `nome_marca` | VARCHAR(250) | Nome da marca |
| `origem` | VARCHAR(255) | País de origem informado |

### `inventario`
| Coluna | Tipo | Descrição |
|---|---|---|
| `id` | INT | Identificador único (chave primária) |
| `modelo` | VARCHAR(250) | Modelo do veículo |
| `transmissão` | VARCHAR(250) | Tipo de transmissão |
| `motor` | VARCHAR(250) | Motorização |
| `combustivel` | VARCHAR(250) | Tipo de combustível |
| `marcas_id` | INT | Chave estrangeira para `marcas.id` |

## 🔗 Relacionamento

Uma **marca** pode estar associada a vários veículos no **inventário** (relacionamento 1:N). A coluna `inventario.marcas_id` referencia `marcas.id` por meio de uma chave estrangeira.

```text
marcas (1) ───────── (N) inventario
   id                    marcas_id

clientes (tabela independente)
```

> Neste estágio do projeto, a tabela `clientes` não possui relacionamento definido com as demais tabelas.

## 🔍 Exemplos de consultas

**Consultar veículos e suas marcas:**

```sql
SELECT
    i.modelo,
    m.nome_marca,
    i.`transmissão`,
    i.motor,
    i.combustivel
FROM inventario AS i
INNER JOIN marcas AS m
    ON i.marcas_id = m.id;
```

**Listar as marcas cadastradas:**

```sql
SELECT id, nome_marca, origem
FROM marcas;
```

**Consultar os clientes cadastrados:**

```sql
SELECT id, nome, sobrenome
FROM clientes;
```

> As consultas acima são exemplos para exploração do banco; não representam necessariamente um histórico de consultas executadas durante o desenvolvimento.

## ▶️ Como executar

1. Instale o **MySQL 8.0** e abra o MySQL Workbench (ou outro cliente SQL compatível).
2. Crie o banco e selecione-o:

   ```sql
   CREATE DATABASE IF NOT EXISTS carplace;
   USE carplace;
   ```

3. Abra o arquivo [`MYSQL-CARPLACE.sql`](MYSQL-CARPLACE.sql) no editor SQL e execute o script.
4. Para verificar os dados, execute:

   ```sql
   SELECT * FROM marcas;
   SELECT * FROM inventario;
   SELECT * FROM clientes;
   ```

**Observação:** o arquivo exportado contém comandos `DROP TABLE IF EXISTS`, que removem tabelas existentes com os mesmos nomes. Execute-o em um banco de testes, sem dados importantes.

## 🎯 Aprendizados

- Modelagem básica de tabelas relacionais
- Chaves primárias e estrangeiras
- Relacionamento 1:N entre tabelas
- Inserção e consulta de registros
- Exportação de um banco MySQL para um arquivo `.sql`

## 🚀 Próximos passos

Possíveis melhorias futuras: cadastrar vendas, relacionar clientes a compras, adicionar informações de preço e estoque e criar consultas para relatórios.

---

**Projeto desenvolvido para fins de estudo e prática em SQL.**
