# Symfony
* Config .env
  ```sh
  # Databse conection url
  # mysql: SGDB Database management system
  # user: Database user
  # passwor: User password
  # 127.0.0.1: Database host
  # 3306: Database port
  # serverVesrion=8: SGDB version
  # charset=urf8mb4: Databse encoding
  DATABASE_URL="mysql://{user}:{password}@{127.0.0.1}:{3306}/app?serverVersion=8&charset=utf8mb4"
  ```
* Libraries
  ```sh
  # Install the package to manage the database
  composer require symfony/orm-pack
  # Install maker library
  composer require --dev symfony/maker-bundle
  # Install serializer
  composer require symfony/serializer-pack
  ```
* Commands
  ```sh
  # Initialize the app server
  symfony serve
  # Create the migration for the entities structure
  symfony console make:migration
  # Create a entity
  symfony console make:entity
  # Create a controller
  symfony console make:controller
  ```
* Doctrine
  ```sh
  # Execute the migration in the database
  symfony console doctrine:migrations:migrate
  ```
