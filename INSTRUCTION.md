Docker Hub:

App: https://hub.docker.com/repository/docker/taniakolesnik/todoapp/tags/2.0.0/sha256-fc905434cd00c7d9ff1d420ad92bb5849be12cf808bed0c0e87be13dcbfcdf6a
Database: https://hub.docker.com/repository/docker/taniakolesnik/mysql-local/tags/1.0.0/sha256:c5d6f6e236d3e2f9df722dd459d1e061cf18de8d79f169a6e081882403c09a31

RUN DATABASE:

docker run -d --name database -p 3306:3306 -v database:/var/lib/mysql taniakolesnik/mysql-local:1.0.0

GET DATABASE LOCAL ADDRESS:

run Command below and get IPv4Address for database container

    docker network inspect bridge

get IPv4Address from relevant container. See example below.

        "605f6990a481fa2353994e06ad3268c3b2658c98be9226808007e990534b3a57": {
                "Name": "database",
                "EndpointID": "dea594b89bb2f89863237d98a3a8b767f2d721a2f800e85a3ebbf749a76c1e9e",
                "MacAddress": "62:7b:10:7c:77:31",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }

Add it into todolist/settings.py as HOST. See example below.

        DATABASES = {
            'default': {
                'ENGINE': 'mysql.connector.django',
                'NAME': 'app_db',
                'USER': 'app_user',
                'PASSWORD': '1234',
                'HOST': '172.17.0.2', 
                'PORT': '', 
        }


RUN APP:

docker run -d --name app -p 8080:8080 taniakolesnik/todoapp:2.0.0

ACCESS APP:

http://localhost:8080