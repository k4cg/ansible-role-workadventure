Role Name
=========

This is a role to deploy [workadventure](https://workadventu.re). By default, a reverse proxy (traefik) with let's encrypt support, front, pusher, and back containers will be deployed. It works by simply taking the docker-compose.prod.yaml file from the master branch of the workadventure repo as a starting point and templating out the values passed to this role. It's also possible to automatically install all stuff that is required on the target server (Debian/Ubuntu only atm).

Requirements
------------

* DNS records pointing to the IP of your reverse proxy
  * play.wa.example.org
  * api.wa.example.org
  * pusher.wa.example.org
* Jitsi Server (meet.jit.si by default)
* Following stuff must be installed on the target server:
  * git (only when setting `env: "dev"`)
  * python >= 3.5
  * pip
  * docker
  * docker-compose installed via pip
  * docker python module

Role Variables
--------------

Please see defaults/mainl.yml for now.

Dependencies
------------

* Collections:
  * community.docker
* Roles:
  * geerlingguy.docker

Dependencies can be installed with `ansible-galaxy install -r requirements.yml`.

Example Playbook
----------------

```yaml
    - name: "Deploy Workadventure"
      hosts: workadventure
      roles:
        - role: '/path/to/ansible-role-workadventure'
          vars:
            install_prerequisites: True # install docker, pip, docker-compose, docker python module, git
            wa_domain: "wa.example.org"
            traefik_acme_email: mail@example.org
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

TODO/IDEAS
----

* Add role variables to README.md
* Add dependencies (docker, docker-compose, evtl. Jitsi und Let's Encrypt) to meta/main.yml?
* Add more config options for traefik?
* Add possibility Use already existing certificates?
* Flag to control if traefik reverse proxy will be deployed?
* Deploy other containers (website, uploader, maps)?
* Possibility to deploy own jitsi server?
* Possibility to deploy own turn server?
* Support installation of prerequisites on other distros
