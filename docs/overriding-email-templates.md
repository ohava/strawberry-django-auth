# Overriding Email Templates

The default email templates are just examples, you probably want to customize it.

## Update your settings:

```python
# settings.py

TEMPLATES = [
    {
        #...
        "DIRS": [os.path.join(BASE_DIR, "templates")],
        # ...
    },
]
```

## File and folder sctructure

Create the following folder and files structure:


```bash hl_lines="3 4 5 6 7 8"
- project_name/
    - project_name/
    - templates/
        email/
          activation_email.html
          activation_subject.txt
          password_reset_email.html
          password_reset_subject.txt
      db.sqlite3
      manage.py
```

Now you can remove ``graphql_auth`` from installed apps:


```diff
    # settings.py

    INSTALLED_APPS = [
      # ...
---   "graphql_auth",
    ]
```

## Email variables

Both subject and email templates receive the following variables:

- user
- token --> activation or password reset
- port
- site_name --> from [django sites framework](https://docs.djangoproject.com/en/3.0/ref/contrib/sites/) <small>(optional)</small>
- domain --> from [django sites framework](https://docs.djangoproject.com/en/3.0/ref/contrib/sites/) <small>(optional)</small>
- protocol
- path --> defined in [settings](/settings) <small>(some frontend path)</small>


## Writing the templates

Write your templates like this:

```html
<!-- activation_email.html -->

<h3>{{ site_name }}</h3>

<p>Hello {{ user.username }}!</p>

<p>Please activate your account on the link:</p>

<p>{{ protocol }}://{{ domain }}/{{ path }}/{{ token }}</p>
```

Provide only the `html` template. It will be converted to `text` later.