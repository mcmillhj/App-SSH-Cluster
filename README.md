[![Build Status](https://travis-ci.org/mcmillhj/App-SSH-Cluster.svg?branch=master)](https://travis-ci.org/mcmillhj/App-SSH-Cluster)
[![Coverage Status](https://coveralls.io/repos/mcmillhj/App-SSH-Cluster/badge.png?branch=master)](https://coveralls.io/r/mcmillhj/App-SSH-Cluster?branch=master)
[![Kwalitee status](http://cpants.cpanauthors.org/dist/App-SSH-Cluster.png)](http://cpants.charsbar.org/dist/overview/App-SSH-Cluster)

# NAME

App::SSH::Cluster - CLI to Net::OpenSSH that runs the same command via SSH on many remote servers at the same time

# VERSION

version 0.004

# SYNOPSIS

    use App::SSH::Cluster;
    App::SSH::Cluster->new_with_options;

# DESCRIPTION

Simple application to execute the same remote command across one or more remote servers. This module does \*not\* handle errors that are generated from remote commands and currently does not log the STDERR of the remote commands that are executed. Any error handling will need to implementing in the calling code.

# NAME 

App::SSH::Cluster

# ATTRIBUTES

- `command`

    command to run on remote servers

- `config_file`

    Absolute path to YAML configuration file that defines the listing of servers, users, and identity-files. If no config\_file is supplied, the default file .app-clusterssh.yml is assumed in the users home directory.

# METHODS

- `run`

    Runs the supplied command (--command <command> or -c <command>) on each remote server. Logging STDOUT to separate files then dumping STDOUT in blocks labelled by the name of the host the STDOUT is from 

# CONFIGURATION

The follow items are required for \*each\* server that you wish to run commands on:

- `identity_file` 

    absolute path to the SSH private key to use to connect 

- `user`

    name of user to connect to remote server as

- `hostname`

    name of remote host

each of these may be defined globally or for each individual server, individual server options take precedence. Global options will be used if any individual options are not listed.

#### EXAMPLE CONFIGURATIONs

    identity_file: "/home/hunter/.ssh/id_rsa"  
    servers:
      - hostname: bastion
        user: hunter
        identity_file: "/home/hunter/.ssh/bastion_rsa"
      - hostname: asphodel
        user: hades

or

    identity_file: "/home/hunter/.ssh/id_rsa"
    user: hunter
    servers:                                 
      - hostname: bastion                    
      - hostname: asphodel
      - hostname: localhost

# AUTHOR

Hunter McMillen <mcmillhj@gmail.com>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2015 by Hunter McMillen.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
