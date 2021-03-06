#openssh

[![Build Status](https://travis-ci.org/vrillusions/puppet-openssh.png?branch=master)](https://travis-ci.org/vrillusions/puppet-openssh)

####Table of Contents

1. [Overview](#overview)
2. [Module Description - What the module does and why it is useful](#module-description)
3. [Setup - The basics of getting started with openssh](#setup)
    * [What openssh affects](#what-openssh-affects)
    * [Setup requirements](#setup-requirements)
    * [Beginning with openssh](#beginning-with-openssh)
4. [Usage - Configuration options and additional functionality](#usage)
5. [Reference - An under-the-hood peek at what the module is doing and how](#reference)
5. [Limitations - OS compatibility, etc.](#limitations)
6. [Development - Guide for contributing to the module](#development)

##Overview

This manages the OpenSSH server.

##Module Description

This manages the configuration of the OpenSSH server. It's defaults fall in line with the [CIS Benchmarks](http://www.cisecurity.org/) and [USGCB](http://usgcb.nist.gov/usgcb/rhel_content.html) benchmarks for ssh servers (as an aside the USGCB link has puppet module downloads. They are... sub-optimal and shouldn't actually be used). As such the defaults are pretty strict and may need adjustment.

##Setup

###What openssh affects

* Install openssh-server and dependencies, which will include openssh-client
* Manage the `sshd_config` file

###Setup Requirements

Currently has no requirements nor dependencies on other modules.

###Beginning with openssh

A simple `include 'openssh'` will suffice.

##Usage

All configuration is done in the main openssh class.  See [Reference](#reference) for a list of options.

##Reference

Hopefully a complete list of parameters that can be set.  These can be set with hiera using `openssh::VAR_NAME` or set when invoking a class.

* `port` - Port it runs on, default 22
* `permit_root_login` - Allow root user to login, default 'no'
* `log_level` - Logging level, default 'INFO'
* `x11_forwarding` - Permit X11 forwarding, default 'no'
* `max_auth_tries` - Number of tries before dropping connection, default 4
* `password_authentication` - Allow the use of passwords to login. Disable this if you only use ssh keys. Default 'yes'
* `ciphers` - List of ssh ciphers to support, defaults to counter based ciphers
* `client_alive_interval` - after this many seconds of no activity increment a count that's used for `client_alive_count_max`. Default is 300 (ie 5 minutes). Setting to 0 disables this. This will probably be a commonly changed option when on dev or staging environments.
* `client_alive_count_max` - when `client_alive_interval` is reached this many times, drop the connection. Default is 0 meaning after the first time `client_alive_interval` is reached, drop the connection.
* `allow_users` - Comma separated list of users to allow. Default is 'UNSET' which excludes this option from config.
* `deny_users` - Comma separated list of users to deny. Default is 'UNSET' which excludes this option from config.
* `banner` - File to display on login. Default is `/etc/issue.net`. Accepts 'UNSET' to not have a login banner
* `sftp_chroot` - Enable sftp chroot settings. Default is false. To take advantage of this create a regular user and place them into the 'sftponly' group. They will then only be able to see their home folder.
* `config_template` - The template file to use for `sshd_config`. This is determined by the module and doesn't need to be set.
* `service_name` - Name of service. Determined by module.
* `service_ensure` - What state should this be in. Default is running
* `service_enable` - Should the service be enabled. Default is true
* `package_name` - Name of package to install. Determined by module.
* `package_ensure` - State of the openssh package. Default is present

##Limitations

Currently testing has been limited to Ubuntu 12.04 and CentOS 5 and 6.  Should work with any debian or redhat flavored OS.

##Development

* Fork
* create feature branch
* make changes
* submit pull requests

