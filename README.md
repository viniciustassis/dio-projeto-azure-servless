# dio-projeto-azure-servless

## Http Trigger
No portal da Azure:
- Criar Logic App
    - Multi-tenant
    - Após recurso criado ir em "Edit"
    - Add Trigger
        - Request: When a HTTP request is received
        - Method: POST
        - Request Body JSON Schema:
        ```json
        {
            "nome": "",
            "idade": 0
        }
        ```
        - Salvar
        - Copiar o endereço de "HTTP URL" para testar via postman

Antes do teste via postman.

### Provisionar uma fila
Ir até o recurso
- Criar um Service Bus

### Obter a chave do service bus
Ir até o recurso
- Overview > Escolher o service bus
- Settings > Shared access policies > Add > Manage (SAS Policy ARM ID) > Copiar connection string Primary connection string

### Criar fila/tópico
Ir até o recurso
- Entities > Queues > Criar
- Também é possível criar uma chave apenas para fila, ao invés da chave para o service bus

- Development Tools
    - Logic app designer
    - Add an action > service bus > send a message
        - settings:
            - Auth type: Access key do service bus ou da fila (queue) (Primary Connection String)
            - Nome da fila ou tópico
        - parameters:
            - Conteúdo: Dynamic content
            - When a HTTP request is received > Body
    - Add an action > Response
        - settings:
            - Status code: 201

## Azure Function Database
- Criar o banco de dados na Azure. Na época do projeto, funciona apenas Mysql.
- Settings > Connection String. Informar na aplicação
- Criar projeto VsCode
- Criar banco tabela ToDo: id, order, title, url, completed
- Criar a pasta de model, classe ToDoItem

### Criar a azure function
No portal da Azure:
- Criar Function App
    - Consumption
    - nome: fn-save-db
- Fazer deploy
    - Na Function App > Overview > Get Publish Profile
    - Importar no VsCode > Publish > Informar o arquivo baixado
    - Criar a variável de ambiente: SqlConnectionString
