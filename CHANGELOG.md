### l5/1.9.2
Merge master from `ba9241426f9c518982d868e2cbac381a9581d802`.

- Refactor EntrustUserTrait to rely on `auth.providers.users.model` instead of `auth.model` (as used upto laravel 5.1) in SoftDeletes checks.
- Updated Docs
    > If your app uses a custom namespace then you'll need to tell entrust where your `permission` and `role` models are, you can do this by editing the config file in `config/entrust.php`

### l5/1.9.1

- Follow Laravel 5.5 conventions in `MigrationCommand` command.
- Utilise the `entrust.permission_foreign_key` and `entrust.role_foreign_key` config in Traits - qualify belongsToMany for Permission Roles.
- Register Provider and Alias in the `extra/laravel` section of composer.json

### l5/1.8.0

- Introduce `entrust.user` and `entrust.users_table` config
- Bypass cache when _file_ or _database_ cache drivers are set. Cache::tags are [not supported for _file_ or _database_ drivers](https://laravel.com/docs/5.5/cache#cache-tags).
- Clean up Middleware parameter handling
    > This updates the middleware to handle the parameters accepted a little better - includes only `explode`ing the values
    when needed and also coercing items expected to be `bool` with `filter_var`.

### l5/1.7.0

- Fix the config reference to the User and Table used in the MigrationCommand
- Introduce `entrust.permission_foreign_key` config

### l5/1.6.0

- Remove `ClassCreatorCommand` as it doesn't exist in main branch and releases.
- Introduce **Cached** code for **Roles** and **Permissions**

- Remove reference to Laravel4 `bootSoftDeletingTrait` and replace the equivalent Laravel 5 SoftDeletes Trait.
  This fix now prevents relationship deletion, where originally relationship deletion occurred. Three traits fixed.

    - `EntrustPermissionTrait` - roles many-to-many
    - `EntrustRoleTrait` - users and permissions many-to-many
    - `EntrustUserTrait` - role many-to-many

    > The traits attach an event listener to remove the many-to-many records on __delete__.
    The intention of SoftDelete trait detection was to __stop the deletion of any records if the permission model uses soft deletes__.

__!! Important !!:__ This fix has potential to the change behaviour by now ( _correctly as intended_ ) preventing deletion 
instead of failing to detect soft deletes and performing deletion.

### l5/1.5.0

- Introduce `entrust.role_foreign_key` config

### l5/1.4.1

- Introduce `entrust.user_foreign_key` config 
