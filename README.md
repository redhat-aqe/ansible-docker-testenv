 ```
     _____________________
    < Ansible Testing PoC >           ______
     ---------------------           < Yay! >
            \   ^__^                  ------
             \  (oo)\_______                \   ,__,
                (__)\       )\/\             \  (oo)____
                    ||----w |                   (__)    )\
                    ||     ||                      ||--|| *
```
---

* test playbook in isolated environment - docker container
    * create image from dockerfile
    * create container
    * create ansible inventory
* launch playbook
    * check mode and/or normal mode
* test container state after playbook has finished
    * should be playbook with asserts
    * assert module
    * block with commands + fail module
    * ... anything that will fail when container is not in expected state
* *N* containers connected to *1* network

```yaml
# setup environment
- hosts: localhost
  roles:
    - role: ansible-testing.setup
      vars:
        hosts:
          - name: foo
            image: localhost/test-image:latest
            command: sleep inf
            volumes:
              - ...
          - ...
      ...

# run playbook we would like to test
- include_playbook: playbook.yml

# run some checks
- ...

# teardown environment
- hosts: localhost
  roles:
    - role: ansible-testing.teardown
      ...
```

## Similar projects

* https://github.com/chrismeyersfsu/provision_docker -- looks good but seems not
  maintained, maybe fork it and improve... (?)
* https://github.com/ansible-community/molecule -- only for roles
