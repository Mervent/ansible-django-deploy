# Django deploy using ansible and docker

Playbook will clone git repo, populate .env file, create dhparams.pem, build and
 start project using  **docker-compose.yml** and **docker-compose.prod.yml**.

## Usage

Create **vars.yml** inside the directory before using the playbook.  
Example is in **vars.example.yml**.

```
ansible-playbook deploy.yml -i myproject.com, -u root
```

## vars.yml

### General settings
**docker_root** - root folder for copying project code  
**project_name** - project name will be used as folder name  
**git_repo** - git repo to use for project cloning

Resulting name will be **docker_root/project_name** for project sources.  
Example: **vars.example.yml** project will be cloned into **/docker/myproject**


### Django specific settings

**django_secret_key** (required) - must be set to a random long value  
**django_allowed_hosts** (required) - must be set to the project domain name  
**django_postgres_passwd** (optional) - better to be set or postgres container
will be using empty password  
**django_sentry_dsn** (optional) - sentry dsn url  
**django_admin_url** (optional) - django admin url, default is 'admin/'

## Troubleshooting

If git clone hangs, make sure your server has access to git repo or
you're forwarding ssh credentials.

```
Host merv.su
  ForwardAgent yes
```

More: https://developer.github.com/v3/guides/using-ssh-agent-forwarding/
