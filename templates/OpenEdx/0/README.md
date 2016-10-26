OpenEdx Stack
=============

#### About OpenEdX
[OpenEdX](https://open.edx.org/) is the LMS platform behind [edX](https://www.edx.org/). An overview of the OpenEdX Architecture can be found [here](https://edx.readthedocs.io/projects/edx-developer-guide/en/latest/architecture.html).

#### About this stack
This stack is based on the OpenEdX docker implementation in the [EdX configuration repo](https://github.com/edx/configuration/tree/master/docker). It has however been modified to allow minor customisations to the config, namely domain names and platform name. The forked repo can be found under [OpensaasAU on github](https://github.com/OpenSaasAU/edx-configuration). The stock docker images (mysql, mongo, rabbitmq, and nginx) were used where ever possible. Edx uses ansible to config and these sripts are set to run on launch to ensure correct configuration.

#### How to use
1. Fill out the custom information and storage locations, note some storage locations are shared between containers so shared storage should be used.
2. Once launched let it run until the EdxappMigrate container has finished, this sets up the mysql database and collects the static assets for nginx to serve, and should take around 15-20mins to complete. This only needs to be run once.
3. Setup an initial django/openedx super user by executing a shell on either lms or cms and running and running the following commands:
```bash
cd /edx/app
source edxapp/edxapp_env
python /edx/app/edxapp/edx-platform/manage.py lms createsuperuser --settings aws
```
For more info on managing the edx application have a [look here](https://openedx.atlassian.net/wiki/display/OpenOPS/Managing+OpenEdX+Tips+and+Tricks)
4. You should be good to go