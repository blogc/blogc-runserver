# blogc-runserver

A simple HTTP server to test blogc websites.

`blogc-runserver` is a simple HTTP server that makes it easy to test blogc websites. Users just need to point it to the directory where the target files where built. It comes with a few pre-defined rules, similar to production webservers, that allow users to quickly test their websites without configuring a webserver.

`blogc-runserver` is part of `blogc` project, but isn't tied to `blogc`. It may be able to serve any website built by static generators.

## Example setup

Download a [release tarball](https://github.com/blogc/blogc-runserver/releases), extract it and enter its directory, after that run the following commands:

    $ ./configure
    $ make
    # make install

Run it:

    $ blogc-runserver ${OUTPUT_DIR}

The binary accepts a few arguments to define the listening port and host. See `blogc-runserver -h` for help.

If some unexpected error happened, please [file an issue](https://github.com/blogc/blogc-runserver/issues/new).

-- Rafael G. Martins <rafael@rafaelmartins.eng.br>
