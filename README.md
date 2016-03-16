Blueflood Finder
================

The BF finder is the graphite plugin that allows graphite and grafana to use blueflood as a backend.

### Setup

To install package from pypi using pip:

    pip install blueflood-graphite-finder

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
    
###Tests

The tests require env variables to be set as follows:

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
