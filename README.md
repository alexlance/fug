fug
===

fug - faster and uglier than fig.

Builds, starts and stops docker containers. Can also be used to 
view the containers' log files when fug is invoked in daemon mode.

### usage


    fug [-b|-d|-k|-l|-c] [-v] [-h]

### options:

    -b      build the services
    -d      run in daemon mode
    -k      kill running containers
    -l      show logs
    -c      configuration file, default: fug.conf
    -v      verbose debugging
    -h      display this help

When run with no arguments, fug will start services in the foreground.
But remember to build (-b) the services first.


### environment

Fug relies on the following environment variable to be set in fug.conf,
for example:

    DOCKER_SERVICES="test db webapp loadbalancer"

Additional settings for each particular container can be specified
with bash arrays:

    declare -A DOCKER_LINKS
    DOCKER_LINKS["webapp"]="db test"
    DOCKER_LINKS["loadbalancer"]="db test webapp"

    declare -A DOCKER_ENV
    DOCKER_ENV["db"]="username password hostname"

And so on for:

    DOCKER_PORTS, DOCKER_VOLUMES, DOCKER_ROOT, DOCKER_EXTRA

The DOCKER_EXTRA array can contain any arbitrary command line
arguments to the docker run command.

To apply a command to all services, use the special service name
ALL. Eg: DOCKER_EXTRA["ALL"]="--rm"


