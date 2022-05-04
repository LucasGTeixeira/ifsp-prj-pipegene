# Setup para rodar o Projeto

## Subindo o Banco de Dados

### Instalando Docker

Caso não tenha docker na sua máquina, instale por aqui a versão mais recente: [Docker](https://www.docker.com/products/docker-desktop/)

### Criando um container docker usando o arquivo docker compose

Partindo da raiz do projeto, rode os seguintes comandos:

```
cd docker
docker-compose up --build --remove-orphans -d

```
O banco já está está sendo populado com alguns dados para facilitar os testes.

É criado um usuário com username: `vini` e senha: `password`.

## Subindo o Front End

A parte do Front End foi construída em Angular e sua instalação e configuração
é detalhada em [Pipegene Front End](httAps://github.com/LucasGTeixeira/pipegene-frontend)

##Subindo os Serviços em Python

Para subir o serviços em python siga as instruções no outro readme do repostitório
[PythonScripts](https://github.com/viniciuslsilva/PipeGeneScripts).

# Pacotes do Projeto

- `configuration:` Define as configurações de execução e segurança usando JSON Web Token como encriptador e autenticação dos tokens criados
- `domain:` Encapsula as classes de domínio do sistema que serão implemetnadas durante a execução da aplicação.
- `external:` Define as Entities e Objetos de acesso a dados que farão conexão com o banco, assim como o envio e recebimento de status dos serviços 
- `usecases: ` Diretório contendo os casos de uso da aplicação, contendo os CRUDs e subdiretórios `gateway`, os quais contém intefaces de Acesso a Dados
- `web:` Define as classes de controladores Rest mapeadas para requisições HTTP no subdiretório `controller`, assim como o tratamento de exceções
dessas requisições no subdiretório `exception`. Para fins de controle, foi criado um subdiretório web chamado `model`, onde as requisições são estuturadas 
em objetos, podendo ser manipuladas e acompanhadas durante o processo de execução das pipelines

## Serviços/Providers da Aplicação (Aplicações Python)

### Grafico de pré-processamento

Com PROVIDER_ID="78cec5db-6396-4fd9-803f-1fd469d76312", ele representa
a app python "app_grafico_pre_processamento.py" que roda na porta 5011. Já existe um projeto chamado
"Explorando pré processamentos MAF" (f2d6a949-8bb5-4df5-8ca7-e5b8d2292488) o qual possui um dataset e uma pipeline configurada
para chamar esse serviço. Ele é o mais simples, recebe um maf e devolve um png.

### Pré-processamento - Rodrigo

Com PROVIDER_ID="e8bf42e4-2ffc-4935-a546-ee5d9263f419", ele representa
a app python "app_pre_processamento_output_maf.py" que roda na porta 5001. A ideia dele é receber um maf de input
e como output devolver um maf, que sera utilizado como input para outro serviço.

### Classificação de variante - Rodrigo

Com PROVIDER_ID="49df4595-b8af-4e32-8791-65e583ae08a2", ele
representa a app python "app_classificacao_variant.py" que roda na porta 5002. A ideia dele é receber um maf de input
resultante de um pre processamento e devolver um png com a classificação da variant.

Ainda na pasta `docker`, entrando em `postgres/sql/V002__populate_schema.sql` tem os scripts para popular a base
com os serviços descritos acima. Lembrando que os ids dos providers são colocados hardcode nas apps python.

