# postman_poc

## TL;DR;

### Pre-Requisitos
- Postman - https://www.postman.com/
- Newman - https://learning.postman.com/docs/postman/collection-runs/command-line-integration-with-newman/
- Newman-Reporter-HTML - https://www.npmjs.com/package/newman-reporter-html

### Scripts
Realize o download de todos os arquivos deste repositório e coloque-os em um mesmo diretório.

### Execução
- Postman
  1. Importar a collection através do arquivo "processo_qa.postman_collection.json" no Postman;
  2. Importar o ambiente através do arquivo "processo_qa.postman_collection.json" na tela de gerenciamento de Ambientes;
  3. Importar as variáveis globais através do arquivo "postman_globals.json" na tela de gerenciamento de variáveis globais;
  4. Dentro do Postman, abrir o Collection Runner da collection previamente importada;
  5. Selecionar o arquivo "data.json" no campo Data;
  6. Clicar no botão para executar os testes.

- Newman
  1. Dentro do diretório onde os arquivos ".json" foram colocados, executar o comando abaixo através de um terminal:
    ```
    newman run processo_qa.postman_collection.json -g postman_globals.json -e qa.postman_environment.json -d data.json -r cli,html
    ```

## Objetivo
O objetivo desta POC é criar uma série de testes utilizando o Postman que visam validar alguns serviços de uma determinada API. Como desafio, esta API requer autenticação e autorização. E os testes, além do Login, foram feitos em um serviço de criação (POST) e um serviço de consulta (GET).

## Instalação
### Postman
O primeiro elemento que precisamos instalar é o Postman. Nele é possível realizar as chamadas à API bem como criar os testes que servirão para validar se o retorno está correto de acordo com o esperado.
- Windows

  Para realizar o download, basta acessar o link https://www.postman.com/downloads/ e clicar em Download.
  Para instalar, execute o arquivo "Postman-winXX-X.XX.X-Setup.exe" obtido no passo anterior e siga os passos sugeridos pelo Instalador.
 
 ### Newman
 O segundo app necessário para esta POC é o Newman, que permite a execução de Collections do Postman através de linha de comando. *Uma pré condição para esta instalação é que tenha o Node.js instalado, para isto, basta seguir os passos do link https://nodejs.org/en/download/.*
- Windows

  Para realizar o download e instalar o Newman, basta executar a linha de comando abaixo em um terminal:
  ```
  npm install -g newman
  ```

 ### Newman-Report-HTML
 Por fim, Newman-Report-HTML que é a biblioteca que permite gerar um relatório das execuções dos teste em um formato "user-friendly". *Assim como o Newman, é necessário ter o Node.js instalado."
-Windows

  Para realizar o download e instalar o Newman-Report-HTML, basta executar a linha de comando abaixo em um terminal:
  ```
  npm install -g newman-reporter-html
  ```
  
 ## Download
 Uma vez que toda a instalação foi concluída, para realizar o download da POC, basta fazer o download (clone) de todos os arquivos ".json" que estão neste repositório e colocá-los em um mesmo diretório. Os arquivos são:
 - processo_qa.postman_collection.json
    - O principal arquivo do projeto que contem a Collection com os serviços, requisições e testes.
 - qa.postman_environment.json
    - Arquivo que contem as variáveis de ambiente utilizadas neste projeto.
 - postman_globals.json
    - Arquivo que contem as variáveis globais utilizadas neste projteo.
 - data.json
    - Arquivo que contem a massa de dados utilzada neste projeto
    
 ## Import
 O próximo passo é carregar o Projeto no Postman. Os passos são os seguintes e devem ser realizados dentro do Postman:
 1. Carregar a Collection 
    1. Clicar em "Import"
    2. Clicar em "Upload Files"
    3. Selecionar o arquivo "processo_qa.postman_collection.json"
    4. Verificar se a Collection com nome "Processo QA" foi listada
    5. Clicar em "Import"
    
 2. Carregar o ambiente
    1. Clicar na engrenagem "Manage Environments"
    2. Clicar em "Import"
    3. Selecionar o arquivo "qa.postman_environment.json"
    
 3. Carregar as variáveis globais
    1. Clicar na engrenagem "Manage Environments"
    2. Clicar em "Import"
    3. Selecionar o arquivo "postman_globals.json"
 Depois de executados os passos acima, a Collection deve estar carregada no Postman, bem como o ambiente QA e todas as variáveis globais.
 
 ## Execução
 Existem duas formas de forma executar os testes desta Collection:
 1. Via Postman
    1. Clicar em "Runner"
    2. Selecionar a Collection "Porcesso QA"
    3. Selecionar o ambiente "QA" no campo "Environment"
    4. Em Data, selecionar o arquivo "data.json"
    5. Clicar em "Start Run"
    
 2. Via Newman
    1. Em um terminal, navegue até o diretório onde o download dos arquivos foi realizado
    2. Execute o comando abaixo:
        ```
        newman run processo_qa.postman_collection.json -g postman_globals.json -e qa.postman_environment.json -d data.json -r cli,html
        ```
        
 ## Resultado
 Em ambas as execuções, 43 testes devem ser executados com sucesso. 
 
 ## Definições da POC
 
 ### Metodologias, Técnicas e Boas Práticas
  - AAA (Arrange, Act, Assert)
      - Para todos os testes, a abordagem de definir toda base de pré-requisitos dos testes previamente, executá-los na sequencia e por realizar a etapa de asserção dos resultados foi adotada para os três serviços testados. 
      
  - Data Driven Testing
      - O arquivo "data.json" serve como input de dados para todos os testes, evitando que a variação de massa tenha que ser realizada dentro do próprio script.
      
  - BDD
      - A linguagem natural foi utilizada para definir o conteúdo de cada um dos testes, de forma que se torna mais fácil identificar o passo executado.

  - Contract Validation
      - Para garantir que todos os campos necessários estão presentes nas respostas, em todos os fluxos os contratos da resposta do serviço foram validados.
      
  - Data Flow Testing
      - Foi utilizado o mecanismo de "data flow" para definir qual fluxo o teste deveria seguir utilizado com base uma valor passado pelo aqruivo de dados através da variável "path". Para este projeto, foram definidos três fluxos: "success", "api_error" e "login_error".
 
 ### Casos de Teste
 Foram definidos 43 Casos de Teste, dividos de acordo com os 3 serviços testados e selecionados através da variável "path" localizada dentro do arquivo "data.json".
 
 Estes Casos de Teste abordaram fluxos de sucesso, onde o retorno do serviço é o correto (200), e fluxos de erros diversos, como falta de acesso, erro interno do servidor e também erro funcional de paramêtro. 
 
#### Login
  - Successo
    - should return a valid json
    - should return a 200 response
    - should return a contract valid for success response
    - should have expires_in equal 3600
    - should have refresh_expires_in equal 1800
    - should have token_type equal bearer
    - should have not-before-policy equal 0
    - should have scope equal profile email
  - Erro (Invalid User)
    - should return a valid json
    - should return a 401 response
    - should return a contract valid for error response
    
  *Os Casos de Teste de Sucesso do serviço Login são executados em dois dos três fluxos ("success" e "api_error").*
 
#### Create Circle
  - Sucesso
    - should return a valid json
    - should return a 200 response
    - should return a contract valid response
    - should have an id with 36 chars
    - should have the same name as the one sent in body
    - should have the same author as the one sent in body
    - should have one clause
  - Erro (Invalid Parameter)
    - should return a valid json
    - should return a 400 response
    - should return a contract valid response
  - Erro (Unauthorized)
    - should return a valid json
    - should return a 401 response
    - should return a contract valid for error response

#### Get Builds
  - Sucesso
    - should return a valid json
    - should return a 200 response
    - should return a contract valid response
    - should have at least a content
    - should be at page 0
  - Erro (Invalid Parameter - Security Test)
    - should return a valid json
    - should return a 500 response
    - should return a contract valid response
  - Erro (Unauthorized)
    - should return a valid json
    - should return a 401 response
    - should return a contract valid for error response
 
 ### Variáveis Locais, de Ambiente e Globais
  - Locais: Variáveis que mudam durante a execução dos testes.
      - access_token: Obtida através do serviço de Login, é utilizada para manter a autenticação do serviço.
      - path: Está no arquivo "data.json", serve para definir o fluxo do teste dentro do script.
      - circle_name: Está no arquivo "data.json", serve para passar como parametro no serviço Create Circle.
      - author_id: Está no arquivo "data.json", serve para passar como parametro no serviço Create Circle.
      - page: Está no arquivo "data.json", serve para passar como parametro no serviço Get Builds.
  - Ambiente: Variáveis que devem ser alteradas apenas se houver mudança de ambiente.
      - login_url: Url base do serviço Login.
      - api_url: Url base dos serviços Create Circle e Get Builds.
      - username: Usuário utilizado para o serviço Login, quando não informado através do arqvuio "data.json".
      - password: Senha utilizada para o serviço Login, quando não informado através do arqvuio "data.json".
  - Globais: Variáveis que devem permanecer sem alteração independente de onde está ocorrendo os testes.
      - login_schema: Contrato de resposta de sucesso do serviço Login.
      - circle_schema: Contrato de resposta de sucesso do serviço Create Circle.
      - build_schema: Contrato de resposta de scuesso do serviço Get Builds.
      - login_error_schema: Contrato de resposta de erro (401) do serviço de Login.
      - api_error_schema: Contrato de resposta de erro de servidor (500) dos serviços Create Circle e Get Builds.
      - missing_fields_schema: Contrato de respota de erro de campos (400) do serviço Create Circle.
        
 
