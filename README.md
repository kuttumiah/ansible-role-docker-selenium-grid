# Ansible Role: Docker Selenium Grid

An Ansible role to create Selenium Grid Server (Hub and Nodes) with Docker images from [SeleniumHQ](https://github.com/SeleniumHQ/docker-selenium).

## Requirements

A host system that has `docker` and `docker-py` installed.

`docker-py` could installed via pip by running `$ sudo pip install docker-py`

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
docker_selenium_tag: latest
docker_selenium_pull_image: false
docker_selenium_state: started
```

Desired `tags` of the images could be used from Docker Registry. Setting `docker_selenium_pull_image: true` will always pull the latest version from the registry.

```yaml
docker_selenium_hub_name: selenium-hub
docker_selenium_hub_port: 4444:4444
docker_selenium_hub_image: selenium/hub
docker_selenium_hub_link: "{{ docker_selenium_hub_name }}:hub"
```

Use docker CLI syntax: 8000, 9000:8000, or 0.0.0.0:9000:8000, where 8000 is a container port, 9000 is a host port, and 0.0.0.0 is a host interface.

```yaml
docker_selenium_nodes:
  - name: selenium-firefox
    image: selenium/node-firefox
    count: 1
  - name: selenium-chrome
    image: selenium/node-chrome
    count: 1
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  vars_files:
    - vars/main.yml
  roles:
    - { role: kuttumiah.docker-selenium-grid }
```

*Inside `vars/main.yml`*:

```yaml
docker_selenium_tag: 3.8.1

docker_selenium_nodes:
  - name: selenium-firefox-debug
    image: selenium/node-firefox-debug
    count: 2
  - name: selenium-chrome-debug
    image: selenium/node-chrome-debug
    count: 2
```

## License

[GNU General Public License v2.0](LICENSE)

## Author Information

This role was created in 2018 by [Md Robaiatul Islam](mailto:robaiat.shaon@gmail.com).
