---
tags: [puppet,query,puppetdb,client,psql]
---

# Quick guide PuppetDB command line client

Prerequisites:

- Workstation with puppet agent installed

- a certficate on the workstation that is signed by your puppet CA-server

- access to TCP-port 8081 of your PuppetDB server.

Furthermore use an account that can read the private key of your puppet certificate.


## Installation

```bash
gem install puppetdb_cli
```

## Configuration

Logged in as the account you're going to use to run the PuppetDB client, create
a file `~/.puppetlabs/client-tools/puppetdb.conf` with the following content:

```
{
  "puppetdb": {
    "server_urls": "https://<puppetdb server>:8081",
    "cacert": "/etc/puppetlabs/puppet/ssl/certs/ca.pem",
    "cert": "/etc/puppetlabs/puppet/ssl/certs/<client host name>.pem",
    "key": "/etc/puppetlabs/puppet/ssl/private_keys/<client host name>.pem"
  }
}
```

## Try it

```bash
puppet query  "nodes [ certname ]{ limit 1 }"
```

## More info

- https://www.puppet.com/docs/puppetdb/7/pdb_client_tools

- https://www.puppet.com/docs/puppetdb/7/api/query/tutorial-pql
