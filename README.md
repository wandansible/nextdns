Ansible role: nextdns
=====================

Install and configure NextDNS DNS to DoH proxy which allows local DNS queries to be
proxied to an upstream DoH server.

Role Variables
--------------

```
ENTRY POINT: main - Install and configure NextDNS DoH proxy

        Install and configure NextDNS DNS to DoH proxy which allows
        local DNS queries to be proxied to an upstream DoH server.

OPTIONS (= is mandatory):

- nextdns_apt_key_fingerprint
        Fingerprint for nextdns apt repo GPG key
        default: AD34842BF3C80F656A833F66467A7CCC8ACFA0B7
        type: str

- nextdns_apt_key_url
        URL for nextdns apt repo GPG key
        default: https://repo.nextdns.io/nextdns.gpg
        type: str

- nextdns_apt_repo
        Entry for nextdns apt repo in sources.list file
        default: https://repo.nextdns.io/deb stable main
        type: str

- nextdns_config
        Contents of the nextdns.conf configuration file, or empty
        string to leave file as is
        default: 'report-client-info false
          auto-activate false
          log-queries false
          cache-size 0
          max-ttl 0s
          bogus-priv true
          timeout 5s
          max-inflight-requests 256
          debug false
          control /run/nextdns/nextdns.sock
          hardened-privacy false
          use-hosts true
          cache-max-age 0s
          mdns all
          discovery-dns
          detect-captive-portals false
          setup-router false
          listen localhost:53'
        type: str

- nextdns_group
        Name of the nextdns unix group
        default: nextdns
        type: str

- nextdns_manage_user
        If true, add nextdns unix user and group
        default: true
        type: bool

- nextdns_user
        Name of the nextdns unix user
        default: nextdns
        type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/nextdns,main,wandansible.nextdns

Or, by adding the following to `requirements.yml`:

    - name: wandansible.nextdns
      src: https://github.com/wandansible/nextdns

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: all
      roles:
         - role: wandansible.nextdns
           become: true
