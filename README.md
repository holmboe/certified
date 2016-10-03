Certified
=========

It's a scary Internet out there.  All your company's internal apps and service-to-service communication should be encrypted.  Certified will help you generate all the certificates you need to make that happen.

Installation
------------

```sh
sudo apt-get install ruby-ronn
sudo make install
```

For some version of `apt-get` and some version of `ruby-ronn`. The point being you need to make sure you have [ronn](https://github.com/rtomayko/ronn) installed.

Or from `packages.rcrowley.org` on Debian or Ubuntu:

```sh
echo "deb http://packages.rcrowley.org $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/rcrowley.list
sudo wget -O /etc/apt/trusted.gpg.d/rcrowley.gpg http://packages.rcrowley.org/keyring.gpg
sudo apt-get update
sudo apt-get -y install certified
```

All you need is `/bin/sh`, GNU `coreutils`, and OpenSSL.

Usage
-----

Generate your CA:

```sh
certified-ca C="US" ST="CA" L="San Francisco" O="Example" CN="Example CA"
```

You're going to want to trust the root CA certificate on all your laptops and servers.  See [Trust your CA](https://github.com/rcrowley/certified/wiki/Trust-your-CA) in the wiki to learn how.

Generate a wildcard certificate:

```sh
certified CN="internal.example.com" +"*.internal.example.com"
```

Generate a certificate with several DNS names:

```sh
certified CN="ops.example.com" +"git.ops.example.com" +"jenkins.ops.example.com"
```

Generate a certificate for an IP address:

```sh
certified CN="localhost" +"127.0.0.1"
```

[Install your certificates](https://github.com/rcrowley/certified/wiki/Install-your-certificates) on all your servers.

The [wiki](https://github.com/rcrowley/certified/wiki) further documents common usage patterns and how to use your CA with various browsers, operating systems, and programming languages.

Advanced topics
---------------

Generate a certificate with an UPN used by Microsoft. Note that `otherName` is case sensitive:

```sh
certified CN="john.doe@example.com" +"otherName:msUPN;UTF8:john.doe@example.com"
```

TODO
----

* Example TLS clients that verify certificates with the CA (in various languages).
* Example TLS servers that use one of these certificates (in various languages).
* Help users with PFS.
* Help users with session resumption.
* Help users run OSCP responders.

TODONE
------

* Generate a CA.
* Generate certificates signed by the CA.
* Generate self-signed certificates.
* Revoke and regenerate certificates.
* Support DNS and IP subject alternative names.
* Prevent invalid DNS names, wildcards, and IPs.
* Commit changes to a Git repository.
* Generate basic CRLs.
* Installer.
* Uninstaller.
* `man` pages.
* Document how to install the CA on Linux.
* Document how to install the CA so browsers can use it.
* Document how to run a CA like Betable's.
* Decouple private keys and certificate signing requests from the signing itself.
* Document GPG-encrypted backups of your CA.
* YAML generator for use with Hiera/Puppet.
* Document how to run an autosigning sub-CA.
* Tag certificates with CRL distribution points and OCSP responder URLs.
* Command for listing every certificate to support automation.
* Document revoking and regenerating the entire CA.
