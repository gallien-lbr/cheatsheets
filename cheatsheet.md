Most often used commands with in my Symfony 4 and Doctrine 2 projects.


| What is does  |  Command |   
|---|---|
|Create a database from scratch|`doctrine:database:create`|
|Create a new entity|`make:entity`|
|Generate a CRUD|`make:crud`|
| Generate a controller | `make:controller`|
|Generate migration file |`make:migration`|
| Applies migration to DB | `doctrine:migrations:migrate`|
| Force a DB update | `doctrine:schema:update –-force ` |
| Generate a form | `make form` |
| Generate a fixture | `make fixture`|
| Load a fixture | `doctrine:fixtures:load -n`|
| Regenerate getters and setters | `make:entity –regenerate` or `make:entity --regenerate App` |
| Regenerate getters and setters for one entity| `make:entity --regenerate App\\Entity\\ChangeTheNameHere`|
| (deprecated) Regenerate getters and setters | `doctrine:generate:entities AppBundle\\Entity\\Shop\\ManyToMany\\TemplateMenu` |
| Debug all routes in  a project | `debug:router` |
| Validate doctrine entities | `doctrine:schema:validate`|
| Install all the vendor | `composer install`|
| Update the packages to their last versions (according to composer.json) | `composer update`|
| Update autoloader (download nothing) | `composer dump-autoload`|

