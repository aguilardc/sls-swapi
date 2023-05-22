### Installation 

Instale módulos npm.

```sh
npm install
```

### Setup Environment

Realice una copia del archivo de variables de entorno `(env.example.yml)` y configure las variables correspondientes.

```sh
cp env.example.yml .env.yml
```
```yaml
development:
  DB_USERNAME: ""
  DB_PASSWORD: ""
  DB_DATABASE: ""
  DB_PORT: 3306
  DB_HOST: "localhost"
  DB_DIALECT: "mysql"
  SWAPI_URL: "https://swapi.py4e.com/api/"
```
Será necesario crear una base de datos.

```sql
CREATE DATABASE swapi;
```
### Migrations

Ejecute las migraciones para la creación de tablas. Estas serán creadas en la base de datos especificada en el archivo *.env.yml* `(DB_DATABASE)`

```sh
npx sequelize-cli db:migrate 
```
### Resources
Los recursos implementados son los siguientes:

- films
- people


##### Films

| Resource / HTTP method | Post             | Get         | Patch                  | Delete             |
| ---------------------- | ---------------- | ----------- | ---------------------- | ------------------ |
| `api/films`            | Create new film  | List films  | Error                  | Error              |
| `api/films/{id}`       | Error            | Get film    | Update user if exists  | Delete film        |

`api/films` acepta el parametro **lang**, especificado con el valor **es**, mapea los campos español, por defecto es ingles.

```bash
http://localhost:8082/development/api/films?lang=es
```

##### People

| Resource / HTTP method | Post             | Get         | Patch                  | Delete             |
| ---------------------- | ---------------- | ----------- | ---------------------- | ------------------ |
| `api/people`           | Create new pers  | List pers | Error                  | Error              |
| `api/people/{id}`      | Error            | Get pers  | Update pers if exists| Delete people      |


### Scripts & Deploy

Para generar los archivos *CloudFormation* ejecute:

```sh
npm run artifacts
```

Configurando adecuadamente las AWS Credentials, el comando `sls deploy` debería desplegar las API's correctamente.
