puppet-dpm module
======

The puppet-dpm module has been developed to ease the set up of a DPM installation via puppet.

It can be used to set up different DPM installations :

 - DPM Headnode ( with or without a local MySql DB)
 - DPM Disknode
 - DPM Head+Disk Node 
 
Dependencies
=====

It relies on several puppet modules, some of them developed @ CERN and some others available from third party.

The following modules are needed in order to use this module, and they are automatically installed from puppetforge

 - lcgdm-gridftp 
 - lcgdm-dmlite
 - lcgdm-lcgdm
 - lcgdm-xrootd
 - lcgdm-voms
 - puppetlabs-stdlib
 - puppetlabs-mysql
 - puppetlabs-firewall
 - saz-memcached
 - CERNOps-bdii
 - CERNOps-fetchcrl
 - erwbgy-limits

Installation
=====

The puppet-dpm module can be installed from puppetforge via

```
puppet module install lcgdm-dpm
```

Usage
=====

The module folder tests contains some examples, for instance you can set up a DPM box with both HEAD and DISK nodes with the following code snippet

```
class{"dpm::head_disknode":
   configure_default_pool => true,
   configure_default_filesystem => true,
   disk_nodes => "localhost",
   localdomain => "cern.ch",
   db_pass => "MYSQLPASS",
   mysql_root_pass => "PASS",
   token_password => "TOKEN_PASSWORD",
   xrootd_sharedkey => "A32TO64CHARACTERKEYTESTTESTTESTTEST",
   site_name => "CERN_DPM_TEST",
   volist =>[dteam],
}
```

the same parameters can be configured via hiera ( see the dpm::params class)

Having the code snippet saved in a file ( i.e.  dpm.pp), then it's just neeed to run:

```
puppet apply dpm.pp
```

to have the DPM box installed and configured
 
Please note that it could be needed to run twice the puppet apply command in order to have all the changes correctly applied
