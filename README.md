# Projeto: Data Warehouse na AWS com Redshift e Looker Studio

Este projeto demonstra uma arquitetura de Data Warehouse na AWS utilizando o Amazon Redshift para ingestão e consulta de dados armazenados no Amazon S3. O objetivo é permitir a análise ad hoc de dados através de dashboards no Looker Studio (antigo Google Data Studio).

---

## 🔧 Tecnologias e Serviços Utilizados

- Amazon Redshift
- Amazon S3
- IAM (papéis e permissões)
- SQL (COPY, criação de tabelas)
- Looker Studio (conexão com Redshift)

---

## 🎯 Objetivo

O projeto consiste em:

1. Armazenar arquivos CSV com dados de vendas em um bucket S3.
2. Criar um cluster Redshift e conectar ao S3 para ingestão dos dados com o comando `COPY`.
3. Criar uma tabela desnormalizada para facilitar análises ad hoc.
4. Conectar o Redshift ao Looker Studio para construção de dashboards.

---

## 🗂️ Estrutura de Pastas

- `sql/`: Scripts SQL para criação e carga de tabelas.
- `imgs/`: Prints de telas da AWS, diagrama da arquitetura e dashboards criados.
- `datasets/`: Exemplo (ou amostra) do dataset utilizado.

---

## 📥 Etapas do Projeto

### 1. Criação do Bucket S3
- Nome único e acesso público bloqueado
- Upload dos arquivos CSV de vendas

![S3](imgs/s3-bucket.png)

---

### 2. Criação do Cluster Redshift
- Tipo: dc2.large
 - ⚠️ Este tipo será descontinuado em abril de 2026
   - Recomenda-se usar RA3 ou Redshift Serverless
- Criação de banco de dados e tabelas

![Redshift](imgs/redshift-cluster.png)

---

### 3. Comando COPY
Script para carregar os dados do S3 para o Redshift:

```sql
COPY vendas
FROM 's3://meu-bucket/vendas.csv'
IAM_ROLE 'arn:aws:iam::123456789012:role/MyRedshiftRole'
CSV
IGNOREHEADER 1;
