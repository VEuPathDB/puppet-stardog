# stardog

A Puppet module to install [Stardog](http://stardog.com) on CentOS.


## Usage:

    include stardog

## Requirements:

Java must be installed on the system. This module does not manage java.

Possibly you will need to open firewall ports. This module does not manage that.

## Parameters

#### `stardog::package_source`

This is a hash with keys

- `url` URL to download stardog zip package. Stardog requires registration
before accessing a temporary download URL. You will need to host the zip
package at a stable, internal location for this module to fetch.

- `sha1` The sha1 checksum for the zip package

Example hiera

      stardog::package_source:
        url: 'http://localhost/stardog/stardog-4.1.zip'
        sha1: '85b3b9e9ebf35cb802a173667984246b3ba11432'

#### `stardog::license_source`

This is a hash with keys

- `url` URL to download stardog license file. Stardog requires registration
before providing a license file. You will need to host the license
file at a stable, internal location for this module to fetch.

- `sha1` The sha1 checksum for the licence file

Example hiera

    stardog::license_source:
      url: 'http://localhost/stardog/stardog-license-key.bin'
      sha1: '9c85394e89a086dfd7d06cb9dc04c828becb9db8'


#### `stardog::java_args`

Java arguments to be passed to the stardog service and also set in
`/etc/profile.d/stardog` for CLI tools. See `STARDOG_JAVA_ARGS` in
Stardog documentation for more information.

#### `stardog::java_home`

Specify `JAVA_HOME` environment variable for stardog service. This
setting will go in `/etc/sysconfig/stardog` (see
`stardog::params::sysconfig`). By default no `JAVA_HOME` is explicitly
set so the stardog service will use the OS default (and if there is no
default the service will fail to start).

#### `stardog::user`

The user that the stardog daemon will run as. This user will be created
unless you set `stardog::manage_user` to false.

#### `stardog::manage_user`

Boolean choice whether to manage the user that the stardog daemon will
run as (`stardog::user`). The default is true.

#### `stardog::version`

The version of Stardog to install. The value must match the value in the
zip package name, i.e. `stardog-${stardog::version}.zip`. The default is
`4.1`.

#### `stardog::home`

The full path to the Stardog working directory of databases and related
files. The default is `/var/lib/stardog`.

#### `stardog::install_dir`

The full path to the directory where Stardog will be installed. The default is
`/opt`.

#### `stardog::port`

#### `stardog::properties`

Optional hash of key value pairs for `$STARDOG_HOME/stardog.properties`
file. A hiera example,

    stardog::properties:
      query.all.graphs: true
      query.timeout: 500ms
