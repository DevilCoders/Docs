# statinfra-api
API for statbox infrastructure


## Local install

    fab venv
    source activate
    # Default should be sqlite; make sure it exists:
    ./manage.py migrate

([Migrations documentation](https://docs.djangoproject.com/en/1.9/topics/migrations/))

To run a local server:

    ./manage.py runserver 127.0.0.1:1234… -v 3 --traceback

([Runserver documentation](https://docs.djangoproject.com/en/1.9/ref/django-admin/#runserver))

If you need to add the local server to an nginx (e.g. on a development server), use proxy_pass:

    location /api/ {
        try_files $uri @api;
    }
    location / {  # optional
        try_files $uri @api;
    }
    location @api {
        client_max_body_size 3000m;
        proxy_connect_timeout 3600s;
        proxy_read_timeout 3600s;
        proxy_send_timeout 3600s;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://localhost:1234…;
        proxy_redirect off;
    }
