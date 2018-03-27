## Overview

This role installs Cantaloupe IIIF server, its dependencies, and some monitoring (which may be broken out later) for use with Islandora (see `./templates/cantaloupe.properties.j2`).

## Configuration
Not much:

- `cantaloupe_host: localhost` for setting up the reverse proxy
- `cantaloupe_http_port: 8182` port cantaloupe should bind to
- `cantaloupe_proxy_host: localhost` for setting up the reverse proxy
- `cantaloupe_version: 3.4.1`
- `cantaloupe_Xmx: 1g` how much memory to allocate
- `monit_install: yes` install monit ?
- `monit_slack_url: https://localhost/slack` url for posting slack updates from monit
- `openjpeg_version: v2.3.0h`

## Testing

Once you've ensured that cantaloupe is serving images, here's a list of commands that make up a spot-check of the build.

    cat /srv/log/application.log # cantaloupe log
    cat /var/log/apache2/cantaloupe-access.log # apache log
    cat /var/log/monit.log    # monit log
    cat /etc/monit/slack-url  # is it correct ?
    less /etc/monit/monitrc   # check for correct interval
    killall java              # test that monit notifies/restarts cantaloupe/notifies
    ll /srv/cache/            # looking around
    ll /srv/cache/source/     # looking around
    ll /srv/cache/info/       # looking around
    df -h                     # headroom ?
    crontab -e                # as root, you should see the cache purge script
