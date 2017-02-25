openwrt-openvpn
===============

configure openvpn aspects of your openwrt system.
compare: [https://wiki.openwrt.org/inbox/vpn.howto]

Dependencies
------------

* [openwrt-uci](https://github.com/flandiGT/openwrt-uci)
* python installed (in ram at least)

What's happening?
-----------------

* Generate CA certificate (if not present)
* Generate Server certificate (if not present)
* Generate TLS Authentication key (if not present)
* Generate Diffie-Hellman parameter (if not present, may take a long time)
* Generate (and download) client certificates and configs
* Setup OpenVPN server

Role Variables
--------------

| variable name     | type   | description/structure                | default |
|-------------------|--------|--------------------------------------|---------|
| ca_key_size       | number | the ca key size in bits              | 2048 |
| ca_expiry         | number | days of ca expiry                    | 3650 |
| ca_country        | text   | the ca country (like US, CA, DE, FR) | US |
| ca_province       | text   | the ca province                      | CA |
| ca_locality       | text   | the ca locality or city              | SanFrancisco |
| ca_org            | text   | the ca organization                  | Fort-Funston |
| ca_email          | text   | the ca email address                 | me@myhost.mydomain |
| ca_org_unit       | text   | the ca organizational unit           | MyOrganizationalUnit |
| key_expiry        | number | days of key expiry                   | 3650 |
| server_address    | text   | your domain name or external ip address | vpn.mydomain.org |
| config_name       | text   | your configuration name                 | my_openvpn_server |
| enabled           | boolean | defines if your configuration is enabed | False |
| clients           | array of texts | the name of your clients         | [] |
| download_dir      | text           | the local download directory     | ./ovpn |
| dev               | text           | the vpn network device           | tun |
| topology          | text           |                                  | subnet |
| proto             | text           | the used transport protocol      | udp |
| port              | number         | the used vpn port                | 1194 |
| server_ip         | ip address as text | the ip address of the vpn server | 10.0.100.1 |
| subnet            | ip address as text | the vpn subnet                   | 10.0.100.0 |
| subnet_mask       | ip address as text | the vpn subnet mask              | 255.255.255.0 |
| clear_all         | boolean            | true = will clear all certificates and keys and rebuild them (include ca, server cert+key, dh param, tlsauth key and client certs+keys) | False |
| clear_ca          | boolean            | true = will clear ca certificate and key and rebuild them (server cert+key and client certs+keys have to be rebuilded too)              | False |
| clear_server_cert | boolean            | true = will clear server certificate and key and rebuild them (client certs+keys have to be rebuilded too)                              | False |
| clear_dh_param    | boolean            | true = will clear dh param and rebuild it (may take a long time)                                                                        | False |
| clear_tlsauth     | boolean            | true = will clear tlsauth key and rebuild it                                                                                            | False |
| clear_client_certs | boolean           | true = will clear client certificates and keys                                                                                          | False |

Example Playbook
----------------

```  
    - role: openwrt-openvpn
      enabled: True
      dev: tun
      config_name: my_openvpn_server
      server_address: vpn.mydomain.org
      port: 1194
      clients:
        - vpnclient01
        - vpnclient02
```

Official documentation:
* [OpenWRT Wiki / OpenVPN server](https://wiki.openwrt.org/inbox/vpn.howto)
* [OpenWRT Wiki / OpenVPN Server HowTo (Streamlined)](https://wiki.openwrt.org/doc/howto/openvpn-streamlined-server-setup)
