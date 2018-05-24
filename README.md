# Network static routes configuration

Ansible role that configures static routes for networking devices. 

The configuration of the role is done so that it shouldn't be necessary to modify the role for any configuration.
All settings can be configured by changing role parameters or by declaring new config as variable.

Please report any issues or send PR.


Details from modules used: 
Cisco NX-OS uses the default VRF for routes if none is defined. VRF names must be shorter than 32 characters and not case sensitive. 
## Examples

```yaml
---

- name: Example of how to add a static route
  hosts: switches
  vars:
    static_routes:
      - prefix: 0.0.0.0/0
        state: present
        next_hop: 192.168.1.1
  roles:
    - Ansible-network_static_route

- name: Example of how to add a couple static routes with next hop name, route tag, admin distance and in specific vrf
  hosts: switches
  vars:
    static_routes:
      - prefix: 0.0.0.0/0
        route_tag: 22
        state: present
        next_hop: 192.168.12.1
        nh_name: oob_switch
        admin_distance: 100
        vrf: mgmt
      - prefix: 10.55.12.0/24
        route_tag: 10
        state: present
        next_hop: 10.11.1.1
        nh_name: firewall
        admin_distance: 100
        vrf: prod
  roles:
    - Ansible-network_static_route


- name: Example of how to remove a static route
  hosts: switches
  vars:
    static_routes:
      - prefix: 0.0.0.0/0
        state: absent
        next_hop: 192.168.1.1
  roles:
    - Ansible-network_static_route
```

## Role variables

```yaml
# Define the static routes to be configured (see README for examples)
static_routes: { }
```


## License

Apache


## Author

Dan Murarasu
