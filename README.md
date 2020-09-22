# Installation

## Code




## Backend

* Démarrer WAMP
* Exécuter les commandes ci-dessous:

```
cd virus-api
composer install
cp .env .env.local
```

* Completer les informations DATABASE_URL, JWT_KEY, API_KEY, API_HOST,MAILJET_SECRET,MAILJET_KEY,SENDER_MAIL

* Migrer la base de données:

```
./bin/console doctrine:migrations:migrate
```

## Frontend

```
cd virus-app
npm install
npm start
now it should work
```
