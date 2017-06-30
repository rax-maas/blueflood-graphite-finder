Blueflood Finder
================

The Blueflood finder is the graphite plugin that allows graphite and grafana to use blueflood as a backend.

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

### Caveat
Blueflood Finder simulates graphite-api. This means we fetch data from blueflood and transform it to graphite-api format:
http://graphite-api.readthedocs.io/en/latest/api.html#rawdata

The graphite-api format is:
```
mycollector.server01.cpuUsage,1306217160,1306217460,60|0.0,0.00666666520965,0.00666666624282,0.0,0.0133345399694
```
The fields are:
```
metric_name,startTime,stopTime,step|comma_separated_values
```

The ```step``` field is in seconds and it is the precision that Grafana or graphite-web will display the graph. If ```step``` is 1, then it will graph the points in 1 second precision.

Blueflood Finder's most granular ```step``` is 60 seconds (for FULL resolution) and its coarsest ```step``` is 86400 (for 1440MIN resolution). 

This means: if you are publishing data more frequently than 60 seconds, they will not show up in Grafana or graphite-web. The best is to adjust your collectors (for example statsd) to flush data every 60 seconds. 

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
    
### Tests

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
