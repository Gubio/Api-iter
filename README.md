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
        "company_id": 1,
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

#### Criar Usuário
    post '/users/'
    cnxs.iter.sc/v1/users/
<details>
<summary>Exemplo:</summary>

```json
{ "user": { "email": "johndoe@example.com" ,"username": "johndoe", "name": "John Doe", "document": "87691457847", "expire_date": "2019-01-01 00:00:00", "phone": "048991618434", "language": "pt-BR", "time_zone": "Brasilia", "company_id": 1, "password": "TheNorthRemembers", "password_confirmation": "TheNorthRemembers", "access_level": 0, "zipcode": "88015203", "street": "R. Menino Deus", "number": "173", "district": "Centro", "city": "Florianópolis", "state": "Santa Catarina", "active": true   }}
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
    cnxs.iter.sc/v1/vehicles/?company_id=1

<details>
<summary>Exemplo:</summary>

```json
[
  {
    "id": 1,
    "name": "DeLorean",
    "description": "",
    "company_id": 1,
    "user_id": 1,
    "plate": "AAA111",
    "mark": "DeLorean",
    "car_model": "DMC-12",
    "year": "1982",
    "color": "gray",
    "fuel": "gasoline",
    "fipe": null,
    "active": true
  },
  {
    "id": 2,
    "name": "V8 Interceptor",
    "description": "",
    "company_id": 1,
    "user_id": 2,
    "plate": "BBB2222",
    "mark": "Ford",
    "car_model": "Falcon XB GT Coupe",
    "year": "1973",
    "color": "black",
    "fuel": "gasoline",
    "fipe": null,
    "active": true
  }
 ]
 ```
</details>

#### Ver Veículo
    get '/vehicles/:id'
    cnxs.iter.sc/v1/vehicles/1
    
<details>
<summary>Exemplo:</summary>

```json
[
  {
    "id": 1,
    "name": "DeLorean",
    "description": "",
    "company_id": 1,
    "user_id": 1,
    "plate": "AAA111",
    "mark": "DeLorean",
    "car_model": "DMC-12",
    "year": "1982",
    "color": "gray",
    "fuel": "gasoline",
    "fipe": null,
    "active": true
  }
 ]
 ```
 
</details>
    
#### Cadastrar Veículo
    post '/vehicles'
    cnxs.iter.sc/v1/vehicles/

<details>
<summary>Exemplo:</summary>

```json

{ "vehicle": {  "name": "DeLorean", "description": " ", "company_id": 1, "user_id": 1, "plate": "AAA111", "mark": "DeLorean", "car_model": "DMC-12", "year": "1982", "color": "gray", "fuel": "gasoline", "fipe": "333", "active": true } }

 ```
 
</details>

    
#### Editar Veículo
    put '/vehicles/:id'
    cnxs.iter.sc/v1/vehicles/1

<details>
<summary>Exemplo:</summary>

```json

{ "vehicle": {  "name": "DeLorean", "description": " ", "company_id": 1, "user_id": 1, "plate": "AAA111", "mark": "DeLorean", "car_model": "DMC-12", "year": "1982", "color": "gray", "fuel": "gasoline", "fipe": "333", "active": true } }

 ```
 
</details>
    
#### Apagar Veículo 
    delete  '/vehicles/:id'
    cnxs.iter.sc/v1/vehicles/1

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
    cnxs.iter.sc/v1/trackers/?company_id=1
    
<details>
<summary>Exemplo:</summary>

```json

{
  "total_count": 207,
  "page_count": 207,
  "page": 1,
  "data": [
    {
      "id": 01,
      "uin": 0000000000001,
      "company_id": 1,
      "vehicle": {
        "name": "DeLorean",
        "type": "car",
        "plate": "AAA111"
      },
      "actions": {
        "vehicle_lock": {
          "enabled": false,
          "labels": {
            "on": "Bloquear Veículo",
            "off": "Desbloquear Veículo"
          }
        },
        "trunk_lock": {
          "enabled": false,
          "labels": {
            "on": "Bloquear Baú",
            "off": "Desbloquear Baú"
          }
        }
      },
      "lat": 0,
      "lng": 0,
      "bearing": 0,
      "speed": 0,
      "ignition": null,
      "temperature": null,
      "gps_time": null,
      "time_pc": null,
      "vehicle_locked": null,
      "trunk_locked": null
    },
    {
      "id": 02,
      "uin": 0000000000002,
      "company_id": 1,
      "vehicle": {
        "name": "V8 Interceptor",
        "type": "car",
        "plate": "BBB2222"
      },
      "actions": {
        "vehicle_lock": {
          "enabled": false,
          "labels": {
            "on": "Bloquear Veículo",
            "off": "Desbloquear Veículo"
          }
        },
        "trunk_lock": {
          "enabled": false,
          "labels": {
            "on": "Bloquear Baú",
            "off": "Desbloquear Baú"
          }
        }
      },
      "lat": 0,
      "lng": 0,
      "bearing": 0,
      "speed": 0,
      "ignition": null,
      "temperature": null,
      "gps_time": null,
      "time_pc": null,
      "vehicle_locked": null,
      "trunk_locked": null
    }]
}
 ```
 
</details>

   
#### Ver Rastreador
    get '/trackers/:uin'
    cnxs.iter.sc/v1/trackers/0000000000001
    
<details>
<summary>Exemplo:</summary>

```json
[
   {
      "id": 01,
      "uin": 0000000000001,
      "company_id": 1,
      "vehicle": {
        "name": "DeLorean",
        "type": "car",
        "plate": "AAA111"
      },
      "actions": {
        "vehicle_lock": {
          "enabled": false,
          "labels": {
            "on": "Bloquear Veículo",
            "off": "Desbloquear Veículo"
          }
        },
        "trunk_lock": {
          "enabled": false,
          "labels": {
            "on": "Bloquear Baú",
            "off": "Desbloquear Baú"
          }
        }
      },
      "lat": 0,
      "lng": 0,
      "bearing": 0,
      "speed": 0,
      "ignition": null,
      "temperature": null,
      "gps_time": null,
      "time_pc": null,
      "vehicle_locked": null,
      "trunk_locked": null
    }
 ]
 ```
 
</details>

#### Cadastrar Rastreador
    post '/trackers'
    cnxs.iter.sc/v1/trackers/
    
<details>
<summary>Exemplo:</summary>

```json

{ "product": {  "uin": "0000000000001", "name": "DeLorean", "company_id": 1, "owner_id": 1, "plate": "AAA111", "mark": "DeLorean", "year": "1982", "color": "gray","active": true } }
 
 ```
 
</details>

#### Editar Rastreador
    put '/trackers/:uin'
#### Apagar Rastreador 
    delete  '/trackers/:id'
