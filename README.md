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


Segue o modelo de dados:

![Script](imgs/ModeloDados.jpg)
---

## 🧭 Arquitetura Geral do Projeto
- Imagem do esquema geral.
![Visão](imgs/Esquema.png)

## 🗂️ Estrutura de Pastas

- `sql/`: Scripts SQL para criação e carga de tabelas.
- `imgs/`: Prints de telas da AWS, diagrama da arquitetura e dashboards criados.
- `datasets/`: Exemplo (ou amostra) do dataset utilizado.

---

## 📥 Etapas do Projeto

### 1. Criação do Bucket S3
- Nome único e acesso público bloqueado
- Upload dos arquivos CSV de vendas


![S3](imgs/buckets3.jpg)

---

### 2. Criação do Cluster Redshift
- Tipo: dc2.large
  - ⚠️ Este tipo será descontinuado em abril de 2026
    - Recomenda-se usar RA3 ou Redshift Serverless
- Criação de banco de dados e tabelas
- Lembre-se de configurar sua security credentials para permitir integração entre Redshift e ferramentas de BI.

![Redshift](imgs/ClusterRedShift.jpg)

---

### 3. Criação de Tabelas SQL no Editor de Consultas Redshift
Script para criação das tabelas que iremos utilizar está na pasta scripts
 - 1.CreateTable

---

### 4. Comando COPY
Script para carregar os dados do S3 para o Redshift:
Abaixo um exemplo geral: Usando apenas uma tabela como base.

```sql
COPY vendas
FROM 's3://meu-bucket/vendas.csv'
'aws_access_key_id='
'aws_secret_access_key='
region 'yyyy'
delimiter ';'
DATAFORMAT 'DD/MM/YYYY'
IGNOREHEADER 1;
```

---

### 5. Desnormalizar Tabelas
Script para desnormalizar as tabelas e tornar consultas com queries menos complexas.
![Script](imgs/ScriptTabelasDesnormalizadas.jpg)

---

### 6. Conectando ao Looker
- Faça o login no Looker
- Conecte os dados com o Amazon RedShift
- Uma vez os dados carregados, podemos criar análises, visualizações Ad Hoc de forma rápida, fácil e interativa.

---

### 7. Reprodução

- Faça upload de arquivos CSV na pasta datasets/ para um bucket S3 em sua conta AWS.
- Crie um cluster Redshift e configure as permissões via IAM.
- Execute os scripts SQL da pasta sql/ para criar e popular as tabelas.
- Utilize os comandos de desnormalização para facilitar análises.
- Conecte o Redshift ao Looker Studio e crie seu dashboard.

---

### 8. Conclusão
- Prática com Data Warehouse em nuvem
- Integração de S3 com Redshift usando copy, mandando as análises em um mesmo ambiente
- Criação de tabelas desnormalizadas para agilizar consultas e análises
- Conexão com ferramentas de BI (Poderiámos ter usado outras ferramentas também)



