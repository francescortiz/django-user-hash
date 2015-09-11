# django-user-hash

Hash system for Django. Features:

- Hashes are associated to users.
- A hash is created for a specific use.
- You associate an optional value to the hash.
- Hashes expire

## Instalation

First install from pipy
    
    pip install django-user-hash
    
Then add 'user_hash' to INSTALLED_APPS.

Finally, migrate database.

    python manage.py migrate user_hash

## Management commands

##### userhash_cleanup

Removes all expired UserHash from databse.

## Usage

To create a new hash:

##### hash = UserHash.create(user, key, value='', duration_seconds=24 * 3600)

Creates a hash instance. In some cases, like in a confirmation for an order, you may have the same key
with different values. Ex: order_confirmation=order-12, order_confirmation=order-32.

- user: Django user to associate the hash to
- key: Key for the hash. (confirmation_email, order_confirmation)
- value: String. Optional.
- duration_minutes: Defaults to 24 hours
- returns the unique hash as a string.

    
##### user, value = UserHash.fetch(hash, key)  

Gets the user and the associated value (if any) of a given hash. Key is mandatory because each hash is created for a specific use. If you want hashes to be used in different cases use the same key everywhere.

##### UserHash.clear(hash)  

Removes a specific hash from database.

##### user, value = UserHash.fetch_and_clear(hash. key)  

Equivalent to calling fetch and clear for a given hash.

##### userhash_list = UserHash.for_user(user, key):

Returns a Django QuerySet that points to all the hashes of a user for a given key.

    

    
