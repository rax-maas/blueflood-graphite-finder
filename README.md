Blueflood Finder
================

The BF finder is the graphite plugin that allows graphite and grafana to use blueflood as a backend.

## Installation

    pip install blueflood-graphite-finder

## Using with graphite-api

In your graphite-api config file:

    finders:
      - blueflood_graphite_finder.blueflood.TenantBluefloodFinder
    blueflood:
      tenant: <tenantid>
      username: <username>
      apikey: <apikey>
      authentication_module: blueflood_graphite_finder.rax_auth
      authentication_class: BluefloodAuth
      urls:
        - https://blueflood-host:port

## Setup

To install manually with code from github repo:
    Get the [blueflood-graphite-finder](https://github.com/rackerlabs/blueflood-graphite-finder) repo from github. Execute the following commands

    cd $REPO_LOCATION
    virtualenv bf-finder
    source bf-finder/bin/activate
    pip install .
 
## Development environment on vagrant

We can setup grafana server on a vagrant vm which visualizes local blueflood using BF finder. To spin up 
vagrant vm use the below commands.

    vagrant box add ubuntu/trusty64
    vagrant up
    
To access grafana, bring your browser up and access the URL: http://192.168.50.4    
    
###Tests

The tests require the following environment variables. Atleast one of no-auth or auth test variables should be set.

For no-auth tests:

       NO_AUTH_URL=<no auth url>
       NO_AUTH_TENANT=<tenant id>

For auth tests:

       AUTH_URL=<blueflood end point>
       AUTH_TENANT=<tenant id>
       AUTH_USER_NAME=<username>
       AUTH_API_KEY=<user's api key>


To run tests, run the below commands
    
    pip install tox
    tox

To run nosetests, run the below commands

    pip install -r blueflood-graphite-finder/test_requirements.txt
    nosetests
    
## Changelog
    
* 1.0.2 (2017-05-31) Fix Grafana display issue for Counters
* 1.0.1 (2016-03-25) Performance improvements for /metrics/find API.
* 1.0.0 (2016-03-23) Base version. 
