# postman_poc

## TL;DR;
### Pre-Requisitos
Postman - https://www.postman.com/
Newman - https://learning.postman.com/docs/postman/collection-runs/command-line-integration-with-newman/
Newman-Reporter-HTML - https://www.npmjs.com/package/newman-reporter-html

### Scripts
Realize o download de todos os arquivos deste repositório e coloque-os em um mesmo diretório.

### Execução
- Postman
1. Importe a collection através do arquivo "processo_qa.postman_collection.json" no Postman
2. Importe o ambiente através do arquivo "processo_qa.postman_collection.json" na tela de gerenciamento de Ambientes
3. Importe as variáveis globais através do arquivo "postman_globals.json" na tela de gerenciamento de variáveis globais
4. Dentro do Postman, abra o Collection Runner da collection previamente importada
5. Selecione o arquivo "data.json" no campo Data
6. Clique no botão para executar os testes

- Newman
1. Dentro do diretório onde os arquivos ".json" foram colocados, execute o comando abaixo através de linda de comando:
'''
newman run processo_qa.postman_collection.json -g postman_globals.json -e qa.postman_environment.json -d data.json -r cli,html
'''
