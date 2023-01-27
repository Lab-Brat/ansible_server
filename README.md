## Ansible Server
Ansible role to deploy and configure infrastructure components such as Docker, Nginx web server, mail relay etc.

#### docker.yaml
Install Docker and Docker Compose.
Demo:
```
ansible-playbook site.yaml --tags 'docker'
```

#### mail.yaml
Sets up SMTP relay with SendGrid API. 
For it to work, a Sendgrid accout with verified `From` address must be registered. 
Playbook is reading API token from environmental variable `SENDMAIL_API`. 
Demo:
```bash
# on the control node
export SENDMAIL_API=<api-token>
ansible-playbook site.yaml --tags 'mail'

# on the host
cat <<EOF > email.txt
Subject: Testing Relay
From: <verified-sendgrid-email>
This is an email relay test
EOF
sendmail < email.txt <send-to-email@mail.com>
```

#### nginx.yaml
Add official Nginx repository and install the web server
Demo:
```
ansible-playbook site.yaml --tags 'nginx'
```

#### selinux_disable.yaml
Disable SELinux for testing purposes.
Demo:
```
ansible-playbook site.yaml --tags 'selinux_off'
```
