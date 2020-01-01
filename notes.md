# Documentation

- [Puppet Product Documenation](https://puppet.com/docs/)
- [Open Source Puppet Doc Index](https://puppet.com/docs/puppet/latest/puppet_index.html)

# General

- Puppet is a configuration management tool to build application stacks from manifests.
- Development process in three iterations:
    1. write initial manifest to install a software package; apply and verify
    2. extend manifest to configure the software installed; apply and verify
    3. add startup logic to get the service running; apply and verify
- Applying a manifest happens in three stages:
    1. compiling the catalogue from manifest
    2. applying the catalogue
    3. producing a report
- Idempotency: applying a manifest once or many times leads to the same result

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

The same as a manifest file (`manifest`):

    user { 'Elisa':
        ensure => 'present',
    }

    puppet apply manifest

Using inline manifest:

    puppet apply --execute "user { 'Elisa': ensure => 'present', }"

Create a manifest from a resource command (also for resources _not_ created by
Puppet, which is very useful for reverse engineering):

    puppet resource user John > user.pp

Create a folder `notes` under `/home/paedu`:

    puppet apply --execute "file { '/home/paedu/notes': ensure => directory; }"

Create an `.exrc` configuration for the new user `nerd`:

    user { 'nerd':
        ensure => 'present',
        managehome => true,
        password => '$6$WDDIVdjTQ2lxv1GI$sIlPPSiJNrZS5WZzFKLq1o9tWThrTQADOxEUURJQlMkz5I3LedBIpG/pbPmXZJqHBwIog2OUOzktol0t7gnJU.',
    }

    file { '/home/nerd/.exrc':
        ensure => 'present',
        content => "set number\nset wrapmargin=80",
    }
