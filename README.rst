Azure alerts monitoring plugin
==============================

Checks azure alerts and raise an alert if some problem is found.
Uses curl with all its power, so you can extend your check with all curl options.

`VERSION  <azure_alerts/VERSION>`__

Install
=======

Linux::

    sudo pip3 install azure_alerts_plugin --upgrade

Also is possible to use::

    sudo python3 -m pip install azure_alerts_plugin --upgrade

On windows with python3.5::

    pip install azure_alerts_plugin --upgrade

For proxies add::

    --proxy='http://user:passw@server:port'

Usage
=====

Use the command line::

    > azure_alerts_plugin --help
        usage: azure_alerts_plugin [-h] [---tenant_id [TENANT_ID]] 
                                    [--client_id [CLIENT_ID]]
                                    [--client_secret [CLIENT_SECRET]]
                                    [--suscription_id [SUSCRIPTION_ID]]
                                    [--time_range [TIME_RANGE]]
                                    [-e [EXTRA_ARGS]] 

        optional arguments:
                            -h, --help show this help message and exit
                            [---tenant_id [TENANT_ID]] Header tenant_id
                            [--client_id [CLIENT_ID]] Header client_id
                            [--client_secret [CLIENT_SECRET]] Header client_secret
                            [--suscription_id [SUSCRIPTION_ID]] Header client_id
                            [--time_range [TIME_RANGE]] Header time_range
                            -e [EXTRA_ARGS], --extra_args [EXTRA_ARGS] extra args to add to curl, see curl manpage

Example usage
=============

Example basic usage::

    > azure_alerts_plugin --tenant_id '{tenant_id}' --client_id '{client_id}' --client_secret '{client_secret}' --suscription_id '{suscription_id}' --time_range '{time_range}'

Nagios config
=============

Example command::

    define command{
        command_name  azure_alerts_plugin
        command_line  /usr/local/bin/azure_alerts_plugin --tenant_id '$ARG1$' --client_id '$ARG2$' --client_secret '$ARG3$' --suscription_id '$ARG4$' --time_range '$ARG5$'
    }

With proxy defined

# use azure_alerts_plugin with proxy
    define command{
        command_name azure_alerts_plugin
        command_line https_proxy=http://user:pass@PROXYIP:PORT /usr/local/bin/azure_alerts_plugin --tenant_id '$ARG1$' --client_id '$ARG2$' --client_secret '$ARG3$' --suscription_id '$ARG4$' --time_range '$ARG5$'
        }


Example service::

    define service {
        host_name                       SERVERX
            service_description             service_name
            check_command                   azure_alerts_plugin!{tenant_id}!{client_id}!{client_secret}!{suscription_id}!{time_range}
            use				                generic-service
            notes                           some useful notes
        }

With proxy defined:

    define service {
            host_name                       SERVERX
            service_description             service_name
            check_command                   azure_alerts_plugin_proxy!!{tenant_id}!{client_id}!{client_secret}!{suscription_id}!{time_range}
            use				                generic-service
            notes                           some useful notes 
            } 

You can use ansible role that already has the installation and command: https://github.com/CoffeeITWorks/ansible_nagios4_server_plugins



TODO
====

* Use hash passwords
* Add Unit tests?
