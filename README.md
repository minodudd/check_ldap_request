check_ldap_request
==================

Nagios Plugin - Check if LDAP attribute exist


# Installation

- Simply put the nagios plugin check_ldap_request.pl in your nagios-plugins directory
- Install the perl module using cpan (install Net::LDAP)

# Nagios configuration

> define command{<br />
>        command_name    check_ldap_request<br />
>        command_line    $USER2$/check_ldap_request.pl -H $HOSTADDRESS$ -b "dc=ldap,dc=company,dc=lan" -f "uid=pmavro"<br />
> }<br />
> <br />
> define service{<br />
>          use                             generic-services<br />
>          hostgroup_name                  ldapsrv<br />
>          service_description             LDAP request check<br />
>          check_command                   check_ldap_request<br />
> }

# Usage
> Usage : ./check_ldap -H hostname -b base -f filer [-s scope] [-h]<br />
>         -H : LDAP server hostname or IP<br />
>         -b : Base of LDAP server (ex: "dc=ldap,dc=company,dc=lan")<br />
>         -f : Specify a filter (ex: "uid=pmavro")<br />
>         -s : LDAP Scope (ex: sub)<br />
>         -h : Print this help message

# Examples

> $ ./check_ldap_request.pl -H prd-ldap-srv -b "dc=openldap,dc=mycompany,dc=com" -f "uid=pmavro"<br />
> LDAP request OK - 'uid=pmavro' exists

> $ ./check_ldap_request.pl -H prd-ldap-srv -b "dc=openldap,dc=mycompany,dc=com" -f "cn=foo"<br />
> LDAP request CRITICAL - unable to find 'cn=foo'

