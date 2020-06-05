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
 
 
