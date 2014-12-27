Fug
===

faster and uglier than fig
--------------------------

Builds, starts and stops docker containers. Can also be used to view the docker log
files. Uses ./fug.yml for configuration, which is syntactically similar to Fig's fig.yml.


Why not fIg?
------------

1) I don't like fig.
2) It feels slow. See 1.
3) No support for `docker run --add-host` (yet)
4) Bad debugging experiences
5) No support for environment variables in the config file.
6) Can't stop and start individual containers without bringing down all of them, ridiculous!


Usage
-----

    $(basename $0) [-c FILE] [-d [NAMES]] [-l [NAMES]] [-b [NAMES]] [-s [NAMES]] [-v] [-h]

Options
-------

    -c FILE         config file, default: ./fug.yml
    -d [NAMES]      run in daemon mode
    -l [NAMES]      show logs
    -b [NAMES]      build services
    -s [NAMES]      stop containers
    -v              verbose debugging
    -h              display this help

Info
----

When run with no arguments, fug will start all services (defined by $DOCKER_SERVICES)
in the foreground. If the containers haven't been built yet, fug will attempt to build
them.

To build, run, or stop some particular services, use a space separated list of service
NAMES: eg: fug -d service1 service2; fug -l service1 service2; fug -s service1 service2

If no list of NAMES is specified, then the operation will apply to ALL services. Eg:
fug -b; fug -d; fug -l

Fug looks for a fug.yml file that defines the manner in which docker run is invoked for
each service. The fug.yml file supports environment variables in ${SOMEVAR} format and
has an ALL build target for settings that should be applied to all services.


Finally
-------

Fig's great, it's not some sordid shell hack like fug. Go use fig and complain to them,
and then poke the docker folk, because docker could be a lot better too. In the meantime
I'm going to script my way around the hassles.


