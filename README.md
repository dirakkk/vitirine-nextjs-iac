# vitrine-next Infra As Code

...

## prérequis

### install ansible

[https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pipx](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pipx)

### confirm installation

[https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#confirming-your-installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#confirming-your-installation)

## ajout clé publique

Attention (digitalocean droplet)

Si connexion par mdp KO, connexion depui sla console web
vi /etc/ssh/sshd_config
PasswordAuthentication yes
sudo service ssh restart

ssh-copy-id -i path/to/key.pub username@remoteHost

ou copier à la main dans authorized_keys

## ping target VM

(from control node)

```
ansible testnode -i inventory -m ping
```

## VM et tests du script ansible

Créer une snapshot de la VM (target node) pour rejouer le script pendant les itérations de dév IAC.

![VM snapshot screenshot](./docs/vm-snapshot.png?raw=true)

## Gestion des secrets et GitHub "time-limited token"

[https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/adding-self-hosted-runners](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/adding-self-hosted-runners)

Limite du playbook : récupérer le token fourni par GitHub pour créer le runner, depuis [https://github.com/avergnaud/vitrine-next/settings/actions/runners/new](https://github.com/avergnaud/vitrine-next/settings/actions/runners/new)

ansible-vault create|edit vars/secrets.yml

## run

ansible-playbook -i inventory playbook.yml --ask-vault-pass
