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
<details>
<summary>Exemplo:</summary>

```json
{
  "token": "MqLgkaAX3YD2KB22W8ZK",
  "realtime_channel_name": "3f500ca078d5799617e5e7c40a4fed38c41f270c118d1aa218c8c2eea5e900a2",
  "user": {
    "id": 1,
    "name": "John Doe",
    "company_id": 1,
    "avatar": "http://res.cloudinary.com/iter-telemetria/image/upload/avatar.jpg"
  },
  "access_profile": {
    "block_vehicles": true,
    "lock_trunk": true,
    "monitoring": true,
    "taxi": false
  }
}
```
</details>

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
    cnxs.iter.sc/v1/users/?company_id=1

<details>
<summary>Exemplo:</summary>

```json

[
  {
    "id": 1,
    "company": 1,
    "name": "John Doe",
    "document": 87691457847,
    "email": "johndoe@example.com",
    "phone": "(048) 99161-8434",
    "expire": "2019-01-01T00:00:00.000Z",
    "language": "pt-BR"
  },
  {
    "id": 2,
    "company": 1,
    "name": "Jane Doe",
    "document": 16087637737,
    "email": "janedoe@example.com",
    "phone": "(048) 99616-9642",
    "expire": "2020-01-19T02:00:00.000Z",
    "language": "pt-BR"
  }
]
```
</details>

#### Ver Usuário
    get '/users/:id'
    cnxs.iter.sc/v1/users/1
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
    cnxs.iter.sc/v1/companies

<details>
<summary>Exemplo:</summary>

```json
[
  {
    "id": 1,
    "name": "One Telemetria"
  },
  {
    "id": 2,
    "name": "Two Telemetria"
  }
]
```
</details>

#### Ver Empresa
    get '/companies/:id'
    cnxs.iter.sc/v1/companies/1

<details>
<summary>Exemplo:</summary>

```json
{
  "id": 1,
  "name": "One Telemetria",
  "document": "56714555000150",
  "email": "contact@example.com",
  "phone": "(48) 3223-5726",
  "owner": 1,
  "financial": 1
}
```
</details>

#### Criar Empresa
    post '/companies/'
    cnxs.iter.sc/v1/companies/

<details>
<summary>Exemplo:</summary>

```json
{ "company": { "name": "Stark Industries", "document": "32991672000100", "email": "hi@stark.com",  "phone": "06232494747", "owner_id": 1, "financial": 1 } }
```

```json
{
  "id": 180,
  "name": "Stark Industries",
  "document": "32991672000100",
  "email": "hi@stark.com",
  "phone": "06232494747",
  "owner": 1,
  "financial": 1
}
```
</details>

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
