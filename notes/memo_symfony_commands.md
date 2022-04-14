# Symfony Commands
Most often used commands with in my Symfony 4 and Doctrine 2 projects.

## Doctrine Related
| Use case | Command |
|---|---|
|Create a database from scratch|`doctrine:database:create`|
| Applies migration to DB | `doctrine:migrations:migrate`|
| Force a DB update | `doctrine:schema:update –-force ` |
| Load a fixture | `doctrine:fixtures:load -n`|
| Validate doctrine entities | `doctrine:schema:validate`|
| (deprecated , symf3) Regenerate getters and setters | `doctrine:generate:entities AppBundle\\Entity\\Shop\\ManyToMany\\TemplateMenu` |

## Make Bundle Related
| Use case | Command |
|---|---|
|Generate a CRUD|`make:crud`|
| Generate a controller | `make:controller`|
|Generate migration file |`make:migration`|
| Generate a form | `make form` |
| Generate a fixture | `make fixture`|
|Create a new entity|`make:entity`|
| Regenerate getters and setters | `make:entity –regenerate` or `make:entity --regenerate App` |
| Regenerate getters and setters for one entity| `make:entity --regenerate App\\Entity\\ChangeTheNameHere`|

## Composer Related
| Use case | Command |
|---|---|
| Symfony website |`composer create-project symfony/website-skeleton my_project`|
| Symfony skeleton (microservice, console app, api) | `composer create-project symfony/skeleton my_project` |
| Install all the vendor | `composer install`|
| Update the packages to their last versions (according to composer.json) | `composer update`|
| Update autoloader (download nothing) | `composer dump-autoload`|
| Run composer with unlimited memory | ` php -d memory_limit=-1 composer.phar install` |
| ??| `composer dump-env prod` |
| Symfony install v4.x by default (not v5) | `composer create-project symfony/website-skeleton Stage_App "4.4.*"|

## Misc Utilities   
| Use case | Command |
|---|---|
| Debug all routes in  a project | `debug:router` |
| Clear templating (twig) cache | `cache:clear`|
| See autowiring available classes (filter with grep)  | `debug:autowiring | grep serviceName`|
| Generate translations i18n | `translation:update --force --output-format=xlf en` |
| Manually Generate a password  | `security:encode-password` |


https://yoandev.co/bootstrap-5-avec-symfony-5-et-webpack-encore/
