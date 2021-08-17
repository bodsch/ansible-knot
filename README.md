
# Ansible Role:  `knot`

This role will fully configure and install [knot](https://github.com/CZ-NIC/knot).

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/bodsch/ansible-icinga2/CI)][ci]
[![GitHub issues](https://img.shields.io/github/issues/bodsch/ansible-knot)][issues]
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bodsch/ansible-knot)][releases]

[ci]: https://github.com/bodsch/ansible-knot/actions
[issues]: https://github.com/bodsch/ansible-knot/issues?q=is%3Aopen+is%3Aissue
[releases]: https://github.com/bodsch/ansible-knot/releases


## Requirements & Dependencies


### Operating systems

Tested on

 - Debian 9 and 10
 - Ubuntu 18.04
 - CentOS 8
 - OracleLinux 8


## Role Variables

```yaml

```

```bash
knotc conf-begin
knotc conf-set zone.domain matrix.lan
knotc conf-commit

knotc zone-begin matrix.lan
knotc zone-set matrix.lan @ 7200 SOA dns hostmaster 1 86400 900 691200 3600
knotc zone-set matrix.lan dns 3600 A 172.17.0.2
knotc zone-set matrix.lan blackbox 3600 A 172.17.0.2
knotc zone-set matrix.lan ldap 3600 CNAME blackbox

# knotc zone-set matrix.lan @ 3600 NS dns.matrix.lan.
# knotc zone-set matrix.lan @ 3600 TXT "rubbel die katz"
# knotc zone-set matrix.lan _ipp._tcp 3600 SRV "10 20 631 www"
knotc zone-commit matrix.lan
```

```bash
matrix.lan.             7200    SOA     dns.matrix.lan. hostmaster.matrix.lan. 1 86400 900 691200 3600
_ipp._tcp.matrix.lan.   3600    SRV     10 20 631 blackbox.matrix.lan.
blackbox.matrix.lan.    3600    A       172.17.0.2
dns.matrix.lan.         3600    A       172.17.0.2
ldap.matrix.lan.        3600    CNAME   blackbox.matrix.lan.
```


## Author and License

  - Bodo Schulz

## License

[Apache](LICENSE)

`FREE SOFTWARE, HELL YEAH!`
