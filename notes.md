# Documentation

- [Puppet Product Documenation](https://puppet.com/docs/)
- [Open Source Puppet Doc Index](https://puppet.com/docs/puppet/latest/puppet_index.html)

# General

- Puppet is a configuration management tool to build application stacks from manifests.
- Development process in three iterations:
    1. write initial manifest to install a software package; apply and verify
    2. extend manifest to configure the software installed; apply and verify
    3. add startup logic to get the service running; apply and verify

# Terms

- manifest: Puppet script
- Puppet DSL: Puppet's language
- types: operating system resources (pre-defined and custom)

# Basic Commands

Print version:

    puppet --version

List built-in types:

    puppet describe --list

List attributes of a type (e.g. `user`):

    puppet describe user

Managing resources:

    puppet resource <type> <name> <attr>=<value>

Dry run:

    puppet [command] --noop

## Examples

Create user Elisa:

    puppet resource user Elisa ensure=present

Remove user Elisa:

    puppet resource user Elisa ensure=absent
