fug
===

###fug - faster and uglier than fig.

Builds, starts and stops docker containers. Can also be used to view the
containers' log files when fug is invoked in daemon mode. Looks for fug.yml
for configuration - which is syntactically similar to fig's fig.yml.

###USAGE:

    $(basename $0) [-d] [-l] [-c] [-b NAMES] [-s NAMES] [-v] [-h]

###OPTIONS:
    -d                detach and run in daemon mode
    -l                show logs
    -c                configuration file, default: fug.yml
    -b <NAMES>|ALL    build service(s)
    -s <NAMES>|ALL    stop container(s)
    -v                verbose debugging
    -h                display this help

When run with no arguments, fug will start services in the foreground. If the
containers haven't been built yet, fug will attempt to build them.

The fug.yml file also supports environment variables in \${SOMEVAR} format, and
has an ALL build target, that lets you put settings that should be applied to
all services. Additionally the special word ALL can be used with -b and -s args.

Fug supports the "docker run --add-host" option through the "hosts" token in the
fug.yml file.

