# ansible-role-precheck

   This precheck can be used at the very start of of a playbook to do various OS pre-checks.
   It will require being called with a become: yes since it also tests if your ansible user is able
   to execute commands as root.
   It is also recommended to set `gather_facts: no` as default.

## Role Variables

See also `main.yml` in the `defaults` folder.
  
* `precheck_remote_tmp`   # Set a default for the remote_tmp var  (defaults to /tmp).
* `precheck_filesystems:` # Optional dict of filesystems to check for space thresholds, variable per RHEL version.
* `precheck_message:`     # Customized message when issues are seen, and reported back in the output.
* `precheck_fail_message` # Customized message on the actual failed task.

## Dependencies

* None

## Example Playbook

```yaml
---
- hosts: all
  gather_facts: no
  become: yes
  vars:
    ansible_user: ansible_linux
    precheck_filesystems:
      "7":
        "/var": 400
  roles:
  - name:  ansible-role-precheck
```

# Author Information

royen99