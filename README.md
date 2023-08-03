# Artix s6 init Minetest Server setup

As of this time of writing, there isn't currently a minetest-server-s6 package in Artix's package repos.

This gist will get you started in the meantime.

## Install

1. Files prepended by `minetest-` in their path must go in `/etc/s6/adminsv/` (ex `/etc/s6/adminsv/minetest-log/run`).
2. The `minetest-env.conf` file must be renamed and moved to `/etc/s6/config/minetest.conf`
3. Edit that file so `MINETEST_GAMEID` is set to a minetest game found in `/var/lib/minetest/.minetest/games`
4. Mark both `run` files and `/etc/s6/adminsv/minetest-srv/finish` as executible.
5. Make a simlink inside `/etc/s6/adminsv/minetest-srv/` pointing to `/var/lib/minetest/.minetest`
6. Make an empty directory `/etc/s6/adminsv/minetest-srv/event/`
7. Add the minetest service group to default so it runs on boot
8. reload the s6 database
 
You should now be able to start or stop `minetest`, or even reboot.

## Postgresql

To use postgresql the service must be installed, so be sure that `postgresql-s6` (or whatever it's called) is present on your system.

I won't tell you how to set up postgresql with minetest, but to ensure it starts before `minetest-srv` do this:

1. `mkdir /etc/adminsv/minetest-srv/dependencies.d`
2. `touch /etc/adminsv/minetest-srv/dependencies.d/postgresql`
