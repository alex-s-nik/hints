# Ordering for models

There is an official Django coding style which provides a recommended ordering for models:

- choices
- database fields
- custom manager attributes
- Meta
- def __str__()
- def save()
- def get_absolute_url()
- custom methods

[Source](https://learndjango.com/tutorials/django-best-practices-models)

# Using DB views in Django ORM
[Source](https://rescale.com/blog/using-database-views-in-django-orm/)


## Migrations for views
If you have few migrations, last of those is data migration (for example # 0002) and you want to undo it for edit some data.
First of all do the next:
```
> python manage.py migrate --fake <app_name> 0001
```
Then do data changes. After all do that:
```
> python manage.py migrate <app_name> 0002
```
