Fug
===

Faster and uglier than fig
--------------------------

Builds, starts and stops docker containers. Can also be used to view the docker log
files. Uses ./fug.yml for configuration, which is syntactically similar to Fig's fig.yml.


Why not fig?
------------

1. Fig doesn't seem to have support for `docker run --add-host` (yet?)
2. I haven't had very good debugging experiences with fig.
3. No support for environment variables in fig's config file.
4. Can't stop, build and restart individual containers without bringing down all of them.


Usage
-----

    fug [-c FILE] [-d [NAMES]] [-l [NAMES]] [-b [NAMES]] [-s [NAMES]] [-v] [-h]

Options
-------

    -c FILE         config file, default: ./fug.yml
    -d [NAMES]      run in daemon mode
    -l [NAMES]      show logs
    -b [NAMES]      build services
    -B [NAMES]      build services, without using cache
    -s [NAMES]      stop containers
    -S [NAMES]      stop containers, remove images
    -v              verbose debugging
    -h              display this help

Examples
--------

    # build all services defined in $DOCKER_SERVICES
    fug -b

    # build only some particular services (the -b, -d, -s
    # and -l args can all accept a list of service names)
    fug -b web db loadb

    # run all services (hit ctrl-c/SIGINT to stop them)
    fug

    # run the services in daemon mode (fug -s to stop them)
    fug -d

    # inspect the logfiles of the web service
    fug -l web

    # inspect all logfiles
    fug -l


Info
----

When run with no arguments, fug will start all services (defined by $DOCKER_SERVICES)
in the foreground. If the containers haven't been built yet, fug will attempt to build
them.

If no list of NAMES is specified, then the operation will apply to ALL services. Eg:
`fug -b && fug -d && fug -l` will build, run/daemonize, and display the logs of all
the services defined in the fug.yml file.

Fug looks for a fug.yml file that defines the manner in which `docker run` is invoked for
each service. The fug.yml file supports environment variables in ${SOMEVAR} format and
has an ALL build target for settings that should be applied to all services. See the 
fug.yml file in this repo for an example.


Finally
-------

Fig's great, it's not some sordid shell hack like fug. Go use fig and complain to them,
and then poke the docker folk, because docker could be a lot better too. In the meantime
I'm going to script my way around the hassles.


