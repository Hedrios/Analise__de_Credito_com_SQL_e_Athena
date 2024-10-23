# Análise de Crédito com Python, SQL e Amazon Athena

Este repositório contém o código e os insights de um projeto de análise de crédito, utilizando SQL para realizar consultas no Amazon Athena e Python para visualizações de dados. O objetivo do projeto é explorar dados de clientes de crédito bancário e fornecer insights estratégicos que auxiliem na personalização de produtos financeiros e campanhas de marketing.

# 1. Objetivo

O projeto busca analisar uma base de dados de clientes de uma instituição financeira, extraindo informações importantes sobre perfil de clientes, faixas de renda, comportamento de crédito e mais, com as seguintes finalidades:

• Compreender melhor o público-alvo.

• Fornecer recomendações estratégicas baseadas em dados.

• Melhorar a segmentação de produtos e campanhas.

# 2. Estrutura do Projeto

A estrutura do projeto foi construída com as seguintes etapas:

## 2.1 Manipulação e Análise Inicial dos Dados no Google Colab

• Upload do arquivo CSV: O arquivo de dados foi carregado no Google Colab para análise e pré-processamento.

• Limpeza e transformação dos dados: Após verificar as colunas e o formato dos dados, foram feitas transformações nas colunas de valores e remoção de colunas desnecessárias.

• Novo arquivo CSV gerado: Após a limpeza dos dados, um novo arquivo CSV foi gerado, contendo apenas as informações relevantes para a análise.

## 2.2 Carregamento dos Dados no Amazon S3

• O arquivo CSV final foi carregado no Amazon S3, onde os dados são armazenados e podem ser acessados pelo Amazon Athena.

## 2.3 Consultas e Análises no Amazon Athena

• Criação da Tabela: A tabela foi criada no Amazon Athena para consultas SQL diretas no arquivo CSV armazenado no S3.

• Consultas SQL: Realizamos consultas SQL para explorar os dados e obter insights como a proporção de clientes por gênero, distribuição por faixa salarial, limites de crédito, entre outros.

# 3. Tecnologias Utilizadas

• SQL: Para consultas de dados no Amazon Athena.

• Amazon Athena: Para realizar consultas SQL diretamente sobre dados no S3.

• Amazon S3: Armazenamento dos arquivos CSV.

• Google Colab: Para o pré-processamento e análise inicial dos dados.

• Python (Pandas e Matplotlib): Para a manipulação de dados e criação de gráficos.

# 4. Estrutura de Dados

A tabela de dados contém as seguintes colunas:

• idade: Idade do cliente

• sexo: Sexo do cliente (F ou M)

• dependentes: Número de dependentes do cliente

• escolaridade: Nível de escolaridade do cliente

• salario_anual: Faixa salarial do cliente

• estado_civil: Estado civil do cliente

• tipo_cartao: Tipo de cartão que o cliente possui

• qtd_produtos: Quantidade de produtos comprados nos últimos 12 meses

• iteracoes_12m: Número de interações/transações nos últimos 12 meses

• meses_inativo_12m: Meses inativos nos últimos 12 meses

• limite_credito: Limite de crédito do cliente

• valor_transacoes_12m: Valor total das transações dos últimos 12 meses

• qtd_transacoes_12m: Quantidade de transações nos últimos 12 meses

# 5. Fluxo do Projeto

1. Carregar o arquivo CSV original no Google Colab.

2. Limpeza e transformação dos dados: Tratamento de colunas, remoção de dados irrelevantes e formatação correta dos valores.

3. Salvar o novo arquivo CSV: Após a transformação, um novo arquivo CSV é gerado.

4. Carregar o arquivo CSV no Amazon S3: O arquivo limpo é carregado no S3, pronto para ser consultado no Athena.

5. Realizar consultas SQL no Amazon Athena: As consultas são executadas diretamente no Amazon Athena para extrair insights dos dados.

6. Visualizar os resultados com gráficos no Python: Gráficos de barras e pizza foram gerados no Colab para melhor visualização dos resultados.

# 6. Consultas SQL

Exemplo de Criação da Tabela no Amazon Athena:

CREATE EXTERNAL TABLE IF NOT EXISTS default.credito (
    idade int,
    sexo string,
    dependentes int,
    escolaridade string,
    estado_civil string,
    salario_anual string,
    tipo_cartao string,
    qtd_produtos int,
    iteracoes_12m int,
    meses_inativo_12m int,
    limite_credito float,
    valor_transacoes_12m float,
    qtd_transacoes_12m int
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe' 
WITH SERDEPROPERTIES ('serialization.format' = ',', 'field.delim' = ',')
LOCATION 's3://seu-bucket/';
TBLPROPERTIES ('has_encrypted_data'='false');

Exemplo de Consulta SQL para Proporção de Gênero:

SELECT count(*), sexo FROM credito GROUP BY sexo;

# 7. Visualizações

## Distribuição de Clientes por Faixa Salarial:

• Utilizamos um gráfico de barras para mostrar a distribuição dos clientes nas diferentes faixas salariais.

## Proporção de Clientes por Gênero:

• Um gráfico de pizza foi utilizado para visualizar a proporção de homens e mulheres na base de clientes.

# 8. Conclusões

A análise revelou os seguintes insights estratégicos:

• A maioria dos clientes tem renda abaixo de $40K, sugerindo um foco em produtos acessíveis para essa faixa.

• Homens recebem limites de crédito maiores do que as mulheres, sugerindo um possível viés a ser investigado.

• Apesar da diferença nos limites, homens e mulheres gastam de forma similar, o que sugere oportunidades para explorar o crédito entre as mulheres.

Esses insights podem guiar decisões estratégicas sobre novos produtos e campanhas, melhorando a segmentação e o atendimento às necessidades dos diferentes perfis de clientes.

# 9. Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para enviar pull requests ou abrir issues para melhorias.






