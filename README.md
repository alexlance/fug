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
4. No ability to stop, build and restart individual containers without bringing down all of them. It seems.
5. Fug can build containers in parallel (by default) or sequentially (with -v)
6. Fug maintains environment variables across container restarts (fug -d)

Usage
-----

    fug [-c FILE] [-d|-l|-L|-b|-B|-s|-e NAMES] [-v] [-h]

Options
-------

    -c FILE         config file, default: ./fug.yml
    -d [NAMES]      run the services in daemon mode
    -l [NAMES]      show logs
    -L [NAMES]      show logs and exit
    -b [NAMES]      build services
    -B [NAMES]      build services, without using cache
    -s [NAMES]      stop containers
    -e NAME         exec into a container
    -v              verbose debugging
    -h              display this help

Examples
--------

    # run the services in daemon mode (fug -s to stop them)
    fug -d

    # build all services defined in fug.yml
    fug -b

    # build only some particular services (the -b, -d, -s
    # and -l args can all accept a list of service names)
    fug -b web db loadb

    # inspect the logfiles of the web service
    fug -l web

    # inspect all logfiles
    fug -l

Info
----

If no list of NAMES is specified, then the operation will apply to ALL services. Eg:
`fug -b && fug -d && fug -l` will build, run/daemonize, and display the logs of all
the services defined in the fug.yml file.

Fug looks for a fug.yml file that defines the manner in which docker run is invoked for
each service. The fug.yml file supports environment variables in ${SOMEVAR} format.

