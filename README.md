### Proxmox on Hetzner BareMetal with ansible

I made this project just for fun, it allows you to create a proxmox host on Hetzner BareMetal


#### Features

 * Install OPNsense as a router. Fake the MAC Address if tge primary Interface and bridged to WAN
 * SEMI Autoinstall (still in progress..)
 * Create Cloud-INIT Images

#### Requirements

  * Tested on Hetzner Bare Metal EX43 at HEL1 - last run 17.10.2022
  * Server in rescue mode with valid SSH public key

#### Variables

 * `hetzner_pve_luks_pass` [default: `secret` ]: Luks encryption password 
 * `hetzner_pve_ssh_keys` [default: `secret` ]: Your SSH Pubkey to login (openssh,busybox boot)
 * `hetzner_pve_acme_mail` [default: `email@example.com` ]: Mail address for acme by letsencrypt
 * `hetzner_pve_acme_domain` [default: `vmhost.domain.com` ]: fqdn from your vmhost - must reachable from external
 * `hetzner_pve_storagebox_server`: storagebox / cifs account to automount
 * `hetzner_pve_custom_packages`: list of custom packages to install


 * `hetzner_pve_setup_opnsense` [default: `true`]: Provision a OPNsense vm Firewall
 * `hetzner_pve_setup_opnsense_force` [default: `true`]: Destroy the old vm and recreate
 * `hetzner_pve_setup_opnsense_enable_ipv6`  [default: `false`]: Enable IPV6
 * `hetzner_pve_setup_opnsense_settings_lan_dhcpd`  [default: `true`]: Start DHCP on LAN Bridge
 * `hetzner_pve_setup_opnsense_user` [default: `ansible`]: Create a ansible user for ansible
 * `hetzner_pve_network_lan_subnet` [default: 24"]: Internal LAN Subnet
 * `hetzner_pve_network_lan_ip` [default: "192.168.49.2"]: Internal LAN IP for Proxmox 
 * `hetzner_pve_network_vm_lan_ip` [default: "192.168.49.254"]: Internal LAN IP for OPNsense
 * `hetzner_pve_network_vm_lan_dhcp_from` [default: "192.168.49.100"]: OPNsense DHCP range start 
 * `hetzner_pve_network_vm_lan_dhcp_to` [default: "192.168.49.150"]:  OPNsense DHCP range end


#### Howto

* ansible-playbook playbook.yml -i inventory/hosts
* OPNsense reachable only from your Ansible HOST via HTTPS.
  

#### Todos

  * Update root password
  * Hetzner API - set server into rescue mode
  * Simple monitoring via mail
  * ...
  * ...


thanks to https://github.com/extremeshok/xshok-proxmox
