# API iter
  #### Servidor de Homologação
    cnxs.iter.sc

  #### WebSocket de Homologação
    107.170.106.29:8081
    
  #### Versão da api
    v1

# Autenticação por Api Key
    "Authorization: bearer {API_KEY}" 

# Autenticação por usuario/senha
    cnxs.iter.sc/v1/sign_in
    Basic Access Authentication - usuário e senha

## Model User - Usuário

| Attribute |Type | extra |
| ------ | ------ | ------ |
| name | string | |
| company_id | integer | |
| email | string | |
| phone  | string | |
| document  | string | CPF |
| expire_date | datetime | 2019-04-01 03:00:00 |
| active | boolean | |
| language | string | pt-BR, es, en |

#### Listar Usuários
    get '/users' ?company_id=

#### Ver Usuário
    get '/users/:id'
#
    Get >  cnxs.iter.sc/v1/users/2
<details>
<summary>Exemplo:</summary>

```json
{
    "user": {
        "id": 1,
        "name": "John Doe",
        "document": 87691457847,
        "contact": {
          "phone": "(048) 99161-8434",
          "email": "johndoe@example.com"
        },
        "address": {
          "zipcode": 88015203,
          "street": "R. Menino Deus",
          "number": 173,
          "district": "Centro",
          "city": "Florianópolis",
          "state": "Santa Catarina",
          "complement": ""
        },
        "expire": "2019-01-01T00:00:00.000Z",
        "active": true
    }
}
```
</details>

#### Cadastrar Usuário
    post '/users'
#### Editar Usuário
    put '/users/:id'
#### Apagar Usuário
    delete '/users/:id' 

## Model Company - Cliente
| Attribute |Type | extra |
| ------ | ------ | ------ |
| name | string | |
| owner_id | integer | id de usuário proprietário desta empresa  |
| financial_id | integer | id da empresa Financeira / Pagante |
| email | string | |
| phone  | string | |
| document  | string | cpf, cpnj |

#### Listar Empresas
    get '/companies'
#### Ver Empresa
    put '/companies/:id'
#### Cadastrar Empresa
    post '/companies'
#### Editar Empresa
    put '/companies/:id'
#### Apagar Empresa
    delete '/companies/:id' 

## Model Vehicle - Veículo
| Attribute |Type | extra |
| ------ | ------ | ------ |
| name | string | |
| company_id | integer |   |
| plate | string |  |
| mark  | string | |
| car_model  | string |  |
| year | string | |
| color | string | |
| fuel | string | |
| fipe | string | código na tabela FIPE  |
| description | text | |
| active | boolean | |

#### Listar Veículos
    get '/vehicles' ?company_id=
#### Ver Veículo
    get '/vehicles/:id'
#### Cadastrar Veículo
    post '/vehicles'
#### Editar Veículo
    put '/vehicles/:id'
#### Apagar Veículo 
    delete  '/vehicles/:id'

## Model Tracker - Rastreador
| Attribute |Type | extra |
| ------ | ------ | ------ |
| uin | string | UIN / IMEI do rastreador |
| company_id | integer |   |
| owner_id | integer | Id do usuário proprietario  |
| name | string |  |
| description | text | Anotações gerais |
| active | boolean | |

#### Listar Rastreadores
    get '/trackers' ?company_id=
#### Ver Rastreador
    get '/trackers/:uin'
#### Cadastrar Rastreador
    post '/trackers'
#### Editar Rastreador
    put '/trackers/:uin'
#### Apagar Rastreador 
    delete  '/trackers/:id'
