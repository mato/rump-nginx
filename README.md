# rump-nginx

## What is this?

Nginx packaging and supporting infrastructure for running as Unikernels atop
the Xen hypervisor, powered by [rumprun](http://repo.rumpkernel.org/rumprun)
and [Rump Kernels](http://rumpkernel.org).

Many thanks to Samuel Martin (@tSed) for developing patches to improve the
cross-compilation support for Nginx.

## Trying it out

To play with this, build rumprun for Xen according to the
[instructions](http://wiki.rumpkernel.org/Repo%3A-rumprun) and add the
`app-tools` directory to your `$PATH`. 

You will also need to install:
* `genisoimage`, to build the data images for the domUs.

To build the nginx unikernel and data images, run:
````
RUMPRUN_CC=rumprun-xen-cc make
````

The resulting unikernel will be left in `bin/nginx`.

To start a domU running nginx, as root run (for example):

````
rumprun xen -M 128 -di \
    -n inet,static,10.10.10.10/24 \
    -b images/stubetc.iso,/etc \
    -b images/data.iso,/data \
    -- bin/nginx -c /data/conf/nginx.conf
````

Comments, questions, criticism welcome at the Rump Kernel mailing list or IRC:
http://wiki.rumpkernel.org/Info:-Community
