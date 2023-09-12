![img](https://avatars1.githubusercontent.com/u/5365410?s=75) Users and Results REST API
======================================

[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)
[![Minimum PHP Version](https://img.shields.io/badge/php-%5E8.1-blue.svg)](http://php.net/)
[![PHPUnit Tests](https://github.com/FJavierGil/miw-api-usuarios/actions/workflows/php.yml/badge.svg)](https://github.com/FJavierGil/miw-api-usuarios/actions/workflows/php.yml)
> 🎯 Implementation of a REST API using the Symfony framework for managing users and results.

This application implements a [REST][rest] API developed as an example of using the [Symfony][symfony] framework. The application provides common operations for managing entities (users and results). This project uses various components of the Symfony framework, [JWT][jwt] (JSON Web Tokens), the [Monolog][monolog] logger, and the [Doctrine ORM][doctrine].

To simplify data management, the [Doctrine][doctrine] ORM has been used. Doctrine 2 is an Object-Relational Mapper that provides transparent persistence for PHP objects. It uses the [Data Mapper][dataMapper] pattern to achieve complete decoupling between business logic and data persistence in database management systems.

Additionally, a partial API specification (OpenAPI 3.0) is included. This specification was created using the [Swagger][swagger] editor. Furthermore, the user interface (SwaggerUI) of this fantastic tool is included, allowing for interactive testing in a complete and elegant manner.

## 🚀 Installation of the Application

The first step is to create an empty database schema and a user/password with full privileges for that schema.

Next, you should create a copy of the `./.env` file and rename it to `./.env.local`. Then, edit this file and modify the `DATABASE_URL` variable with the following parameters:

- Username and password of the user generated earlier.
- Name of the database schema.

Once you've edited the file, run the following commands from the root directory of the project:

```shell
$ composer update
$ php bin/console doctrine:schema:update --dump-sql --force

The base project provided includes the [lexik/jwt-authentication-bundle][lexik] component for generating JWT tokens. Following the instructions provided in the [documentation][1] of this component, you should generate the necessary SSH keys with the following commands:
```
$ mkdir -p config/jwt
$ openssl genpkey -out config/jwt/private.pem -aes256 -algorithm rsa -pkeyopt rsa_keygen_bits:4096
$ openssl pkey -in config/jwt/private.pem -out config/jwt/public.pem -pubout
```
In XAMPP installation, the openssl program can be found in the XAMPP/apache/bin directory. The rest of the configuration has already been done in this project. Use the passphrase specified in the JWT_PASSPHRASE variable in the .env file.

To launch the development server with the application, run the following command from the project's root directory:
$ symfony serve [-d]
```
Before testing the API interface, it is recommended to create at least one user with administrator permissions. To achieve this, a command is provided through the Symfony console. You can get the description of how this command works with:
$ php bin/console miw:create-user --help
```
You can now make a request with your browser to the address https://127.0.0.1:8000/.

🗄️ Project Structure:
The content and structure of the project are as follows:

Root directory of the project .:
.env: Default local environment variables.
phpunit.xml.dist: Default configuration for the test suite.
README.md: This file.
bin directory:
Executables (console and phpunit).
src directory:
Contains the source code of the application.
Subdirectory src/Entity: PHP entities (includes ORM mapping annotations).
var directory:
Log and cache files (separated by environments).
public directory:
index.php is the front controller of the application. It initializes and launches the core of the application.
Subdirectory api-docs: [Swagger][swagger] client and API specification.
vendor directory:
Components developed by third parties (Symfony, Doctrine, JWT, Monolog, Dotenv, etc.).
tests directory:
A set of scripts for running unit and integration tests with PHPUnit.
🛠️ Running Tests
The application includes a set of tools for running unit and integration tests with PHPUnit. Using these tools, you can automatically verify the correct functionality of the entire API without the need for additional tools.

To set up the testing environment, create an empty database schema and make a copy of the ./phpunit.xml.dist file, renaming it to ./phpunit.xml. Similarly, create a copy of the ./.env.test file and rename it to ./.env.test.local. Then, edit this file to assign the following parameters:

Additionally, to check the quality of the tests, the project includes mutation tests generated using the Infection tool. The process is simple: small changes are made to the original code (mutants), and then the test suite is executed. If the tests fail, it means they were able to detect the code modification, and the mutant is eliminated. If the tests pass, the mutant survives, and the reliability of the test is questioned.

To run mutation tests, execute:
> composer infection
```

Finally, two tools for static code analysis, [PHPStan][phpstan] and [PhpMetrics][phpmetrics], have been added. PhpStan is a static code analysis tool, while PhpMetrics analyzes the code and allows you to generate reports with various project metrics. These tools can be run using the following commands:
> composer phpstan
> composer metrics
```

[dataMapper]: http://martinfowler.com/eaaCatalog/dataMapper.html
[doctrine]: http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/
[infection]: https://infection.github.io/guide/
[jwt]: https://jwt.io/
[lh]: https://127.0.0.1:8000/
[monolog]: https://github.com/Seldaek/monolog
[openapi]: https://www.openapis.org/
[phpunit]: http://phpunit.de/manual/current/en/index.html
[rest]: http://www.restapitutorial.com/
[symfony]: https://symfony.com/
[swagger]: http://swagger.io/
[yaml]: https://yaml.org/
[lexik]: https://github.com/lexik/LexikJWTAuthenticationBundle
[1]: https://github.com/lexik/LexikJWTAuthenticationBundle/blob/master/Resources/doc/index.md#generate-the-ssh-keys
[phpstan]: https://phpstan.org/
[phpmetrics]: https://phpmetrics.org/
