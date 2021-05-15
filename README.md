# Ansible Role: Nameserver

This role sets up a Linux server to be a DNS Server.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: ansible-role-nameserver
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`)

Switch for first installation.

    nameserver_installation: 'false'

Configure DNS Server IP and Network Adress.

    nameserver_ip: '192.168.178.2'
    nameserver_network: '192.168.178.0/24'

Configure List of `/etc/named.conf` Includes.

    nameserver_named_includes:
      - 'include "/etc/named/named.conf.local";'

Name DNS Zones.

    nameserver_default_zone: 'home.lab'
    nameserver_reverse_zone: '178.168.192.in-addr.arpa'

Manage DNS Records (begin with ID 3!)

    dns_records:
      - id: 3
        host: host101
        type: A
        ip: 192.168.1.101


## Dependencies

Ansible Collection: ansible.posix

    - name: ansible.posix
      type: galaxy
      source: https://galaxy.ansible.com

## OS Compatibility

This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    role_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run nameserver role."
      hosts: all
      become: yes
      roles:
        - ansible-role-nameserver

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2021 by [ButlerMiles](https://github.com/ButlerMiles/).
