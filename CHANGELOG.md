## [1.0.0.beta1](https://github.com/fgrehm/vagrant-lxc/compare/v0.8.0...master) (unreleased)

DEPRECATIONS:

  - Support to **all Vagrant versions prior to 1.5 are now deprecated**, there is a
    [small layer](lib/vagrant-backports) that ensures compatibility with versions
    starting with 1.1.5 but there is no guarantee that it will stick for too long.
  - Boxes released prior to this version are now deprecated and won't be available
    after the final 1.0.0 release.
  - `--auth-key` argument is no longer provided to `lxc-template`. This will cause
    all official base boxes prior to 09/28/2013 to break.

FEATURES:

  - Support for NFS and rsync synced folders.
  - Support for synced folder mount options allowing for using read only synced
    folders [[GH-193]]

[GH-193]: https://github.com/fgrehm/vagrant-lxc/issues/193

IMPROVEMENTS:

  - `lxc-template` is now optional for base boxes and are bundled with the plugin,
    allowing us to roll out updates without the need to rebuild boxes [[GH-254]]
  - Set container's `utsname` to `config.vm.hostname` by default [[GH-253]]
  - Added libvirt dnsmasq leases file to the lookup paths [[GH-251]]
  - Improved compatibility with Vagrant 1.4 / 1.5 including the ability
    to use `rsync` and `nfs` shared folders to work around synced folders
    permission problems. More information can be found on the following
    issues: [[GH-151]] [[GH-191]] [[GH-241]] [[GH-242]]
  - Warn in case `:group` or `:owner` are specified for synced folders [[GH-196]]
  - Acceptance specs are now powered by `vagrant-spec` [[GH-213]]

[GH-254]: https://github.com/fgrehm/vagrant-lxc/issues/254
[GH-196]: https://github.com/fgrehm/vagrant-lxc/issues/196
[GH-251]: https://github.com/fgrehm/vagrant-lxc/pull/251
[GH-253]: https://github.com/fgrehm/vagrant-lxc/pull/253
[GH-151]: https://github.com/fgrehm/vagrant-lxc/issues/151
[GH-213]: https://github.com/fgrehm/vagrant-lxc/issues/213
[GH-191]: https://github.com/fgrehm/vagrant-lxc/issues/191
[GH-241]: https://github.com/fgrehm/vagrant-lxc/issues/241
[GH-242]: https://github.com/fgrehm/vagrant-lxc/issues/242


BASE BOXES:

  - Switched to [`lxc-download`](https://github.com/lxc/lxc/blob/master/templates/lxc-download.in)
    as the "reference implementation" for the generic `lxc-template` script [[GH-236]]
  - Added support for _appending_ custom boxes configs with the `lxc-config` file,
    allowing usage of host's specific configs from `/etc/lxc/default.conf` [[GH-222]]
  - Include NFS client on Ubuntu and Debian base boxes [[GH-218]]
  - Improved output for building base boxes
  - Improved `vagrant` user `sudo` rights [[GH-231]] [[GH-188]]
  - Locale configuration may follow builder's LANG environment variable [[GH-221]]
  - Enable bash completion for Debian base boxes [[GH-220]]
  - Fix broken locale in Ubuntu boxes [[GH-201]]
  - Install `python-software-properties` by default [[GH-155]]
  - Fix apt-get error when building Ubuntu boxes [[GH-200]]

[GH-236]: https://github.com/fgrehm/vagrant-lxc/issues/236
[GH-222]: https://github.com/fgrehm/vagrant-lxc/issues/222
[GH-218]: https://github.com/fgrehm/vagrant-lxc/issues/218
[GH-231]: https://github.com/fgrehm/vagrant-lxc/issues/231
[GH-221]: https://github.com/fgrehm/vagrant-lxc/issues/221
[GH-220]: https://github.com/fgrehm/vagrant-lxc/issues/220
[GH-201]: https://github.com/fgrehm/vagrant-lxc/issues/201
[GH-188]: https://github.com/fgrehm/vagrant-lxc/issues/188
[GH-155]: https://github.com/fgrehm/vagrant-lxc/issues/155
[GH-200]: https://github.com/fgrehm/vagrant-lxc/issues/200


## [0.8.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.7.0...v0.8.0) (Feb 26, 2014)

FEATURES:

  - Support for naming containers from Vagrantfiles [#132](https://github.com/fgrehm/vagrant-lxc/issues/132)

IMPROVEMENTS:

  - Use a safer random name for containers [#152](https://github.com/fgrehm/vagrant-lxc/issues/152)
  - Improve Ubuntu 13.10 compatibility [#190](https://github.com/fgrehm/vagrant-lxc/pull/190) / [#197](https://github.com/fgrehm/vagrant-lxc/pull/197)
  - Improved mac address detection from lxc configs [#226](https://github.com/fgrehm/vagrant-lxc/pull/226)

BUG FIXES:

  - Properly detect if lxc is installed on hosts that do not have `lxc-version` on their paths [#186](https://github.com/fgrehm/vagrant-lxc/issues/186)


## [0.7.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.6.4...v0.7.0) (Nov 8, 2013)

IMPROVEMENTS:

  - Support for `vagrant up` in parallel [#152](https://github.com/fgrehm/vagrant-lxc/issues/152)
  - Warn users about unsupported private / public networking configs [#154](https://github.com/fgrehm/vagrant-lxc/issues/154)
  - Respect Vagrantfile options to disable forwarded port [#149](https://github.com/fgrehm/vagrant-lxc/issues/149)

BUG FIXES:

  - Nicely handle blank strings provided to `:host_ip` when specifying forwarded ports [#170](https://github.com/fgrehm/vagrant-lxc/issues/170)
  - Fix "Permission denied" when starting/destroying containers after lxc
    security update in Ubuntu [#180](https://github.com/fgrehm/vagrant-lxc/issues/180)
  - Fix `vagrant package` [#172](https://github.com/fgrehm/vagrant-lxc/issues/172)


## [0.6.4](https://github.com/fgrehm/vagrant-lxc/compare/v0.6.3...v0.6.4) (Oct 27, 2013)

FEATURES:

  - New script for building OpenMandriva base boxes [#167](https://github.com/fgrehm/vagrant-lxc/issues/167)

IMPROVEMENTS:

  - Make `lxc-template` compatible with Ubuntu 13.10 [#150](https://github.com/fgrehm/vagrant-lxc/issues/150)

BUG FIXES:

  - Fix force halt for hosts that do not have `lxc-shutdown` around (like Ubuntu 13.10) [#150](https://github.com/fgrehm/vagrant-lxc/issues/150)

## [0.6.3](https://github.com/fgrehm/vagrant-lxc/compare/v0.6.2...v0.6.3) (Oct 12, 2013)

IMPROVEMENTS:

  - Respect Vagrantfile option to disable synced folders [#147](https://github.com/fgrehm/vagrant-lxc/issues/147)

BUG FIXES:

  - Fix error raised when fetching container's IP with the sudo wrapper disabled [#157](https://github.com/fgrehm/vagrant-lxc/issues/157)

## [0.6.2](https://github.com/fgrehm/vagrant-lxc/compare/v0.6.1...v0.6.2) (Oct 03, 2013)

IMPROVEMENTS:

  - Cache the result of `lxc-attach --namespaces` parameter support checking to
    avoid excessive logging.

BUG FIXES:

  - Fix detection of `lxc-attach --namespaces` parameter support checking.

## [0.6.1](https://github.com/fgrehm/vagrant-lxc/compare/v0.6.0...v0.6.1) (Oct 03, 2013)

IMPROVEMENTS:

  - Fall back to `dnsmasq` leases file if not able to fetch IP with `lxc-attach` [#118](https://github.com/fgrehm/vagrant-lxc/issues/118)
  - Make sure lxc templates are executable prior to `lxc-create` [#128](https://github.com/fgrehm/vagrant-lxc/issues/128)
  - New base boxes with support for lxc 1.0+

BUG FIXES:

  - Fix various issues related to detecting whether the container is running
    and is "SSHable" [#142](https://github.com/fgrehm/vagrant-lxc/issues/142)
  - Nicely handle missing templates path [#139](https://github.com/fgrehm/vagrant-lxc/issues/139)

## [0.6.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.5.0...v0.6.0) (Sep 12, 2013)

IMPROVEMENTS:

  - Compatibility with Vagrant 1.3+ [#136](https://github.com/fgrehm/vagrant-lxc/pull/136)
  - Set plugin name to `vagrant-lxc` so that it is easier to check if the plugin is
    installed with the newly added `Vagrant.has_plugin?`

BUG FIXES:

  - Fix box package ownership on `vagrant package` [#140](https://github.com/fgrehm/vagrant-lxc/pull/140)
  - Fix error while compressing container's rootfs under Debian hosts [#131](https://github.com/fgrehm/vagrant-lxc/issues/131) /
    [#133](https://github.com/fgrehm/vagrant-lxc/issues/133)

## [0.5.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.4.0...v0.5.0) (Aug 1, 2013)

BACKWARDS INCOMPATIBILITIES:

  - To align with Vagrant's core behaviour, forwarded ports are no longer attached
    to 127.0.0.1 and `redir`'s `--laddr` parameter is skipped in case the `:host_ip`
    config is not provided, that means `redir` will listen on connections coming
    from any of the host's IPs.

FEATURES:

  - Add support for salt-minion and add latest dev release for ubuntu codenamed saucy [#116](https://github.com/fgrehm/vagrant-lxc/pull/116)
  - Add support for using a sudo wrapper script [#90](https://github.com/fgrehm/vagrant-lxc/issues/90)
  - `redir` will log to `/var/log/syslog` if `REDIR_LOG` env var is provided

IMPROVEMENTS:

  - Error out if dependencies are not installed [#11](https://github.com/fgrehm/vagrant-lxc/issues/11) / [#112](https://github.com/fgrehm/vagrant-lxc/issues/112)
  - Support for specifying host interface/ip for binding `redir` [#76](https://github.com/fgrehm/vagrant-lxc/issues/76)
  - Add Vagrantfile VM name to the container name [#115](https://github.com/fgrehm/vagrant-lxc/issues/115)
  - Properly handle forwarded port collisions [#5](https://github.com/fgrehm/vagrant-lxc/issues/5)
  - Container's customizations are now written to the config file (usually
    kept under `/var/lib/lxc/CONTAINER/config`) instead of passed in as a `-s`
    parameter to `lxc-start`

## [0.4.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.3.4...v0.4.0) (Jul 18, 2013)

FEATURES:

  - New box format [#89](https://github.com/fgrehm/vagrant-lxc/issues/89)

BUG FIXES:

  - Add translation for stopped status [#97](https://github.com/fgrehm/vagrant-lxc/issues/97)
  - Enable retries when fetching container state [#74](https://github.com/fgrehm/vagrant-lxc/issues/74)
  - Fix error when setting Debian boxes hostname from Vagrantfile [#91](https://github.com/fgrehm/vagrant-lxc/issues/91)
  - BTRFS-friendly base boxes [#81](https://github.com/fgrehm/vagrant-lxc/issues/81)
  - Extended templates path lookup [#77](https://github.com/fgrehm/vagrant-lxc/issues/77) (tks to @aries1980)
  - Fix default group for packaged boxes tarballs on the rake task [#82](https://github.com/fgrehm/vagrant-lxc/issues/82) (tks to @cduez)

## [0.3.4](https://github.com/fgrehm/vagrant-lxc/compare/v0.3.3...v0.3.4) (May 08, 2013)

FEATURES:

  - Support for building Debian boxes (tks to @Val)
  - Support for installing babushka on base boxes (tks to @Val)

IMPROVEMENTS:

  - Replace `lxc-wait` usage with a "[retry mechanism](https://github.com/fgrehm/vagrant-lxc/commit/3cca16824879731315dac32bc2df1c643f30d461#L2R88)" [#22](https://github.com/fgrehm/vagrant-lxc/issues/22)
  - Remove `/tmp` files after the machine has been successfully shut down [#68](https://github.com/fgrehm/vagrant-lxc/issues/68)
  - Clean up base boxes files after they've been configured, resulting in smaller packages
  - Bump development dependency to Vagrant 1.2+ series

BUG FIXES:

  - Issue a `lxc-stop` in case the container cannot shutdown gracefully [#72](https://github.com/fgrehm/vagrant-lxc/issues/72)

## [0.3.3](https://github.com/fgrehm/vagrant-lxc/compare/v0.3.2...v0.3.3) (April 23, 2013)

BUG FIXES:

  - Properly kill `redir` child processes [#59](https://github.com/fgrehm/vagrant-lxc/issues/59)
  - Use `uname -m` on base Ubuntu lxc-template [#53](https://github.com/fgrehm/vagrant-lxc/issues/53)

IMPROVEMENTS:

  - Initial acceptance test suite
  - New rake tasks for building Ubuntu precise and raring base amd64 boxes

## [0.3.2](https://github.com/fgrehm/vagrant-lxc/compare/v0.3.1...v0.3.2) (April 18, 2013)

  - Do not display port forwarding message in case no forwarded ports were set

## [0.3.1](https://github.com/fgrehm/vagrant-lxc/compare/v0.3.0...v0.3.1) (April 18, 2013)

  - Improved output to match lxc "verbiage"

## [0.3.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.2.0...v0.3.0) (April 10, 2013)

BACKWARDS INCOMPATIBILITIES:

  - Boxes `lxc-template` should support a `--tarball` parameter
  - `start_opts` config was renamed to `customize`, please check the README for the expected parameters
  - V1 boxes are no longer supported
  - `target_rootfs_path` is no longer supported, just symlink `/var/lib/lxc` to the desired folder in case you want to point it to another partition
  - Removed support for configuring private networks. It will come back at some point in the future but if you need it you should be able to set using `customize 'network.ipv4', '1.2.3.4/24'`

IMPROVEMENTS:

  - lxc templates are removed from lxc template dir after container is created
  - Treat NFS shared folders as a normal shared folder instead of ignoring it so we can share the same Vagrantfile with VBox environments
  - Support for lxc 0.7.5 (tested on Ubuntu 12.04) [#49](https://github.com/fgrehm/vagrant-lxc/issues/49)
  - Remove `/tmp` files when packaging quantal64 base box [#48](https://github.com/fgrehm/vagrant-lxc/issues/48)
  - Avoid picking the best mirror on quantal64 base box [#38](https://github.com/fgrehm/vagrant-lxc/issues/38)

BUG FIXES:

  - Redirect `redir`'s stderr output to `/dev/null` [#51](https://github.com/fgrehm/vagrant-lxc/issues/51)
  - Switch from `ifconfig` to `ip` to grab container's IP to avoid localization issues [#50](https://github.com/fgrehm/vagrant-lxc/issues/50)

## [0.2.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.1.1...v0.2.0) (March 30, 2013)

  - Experimental box packaging (only tested with Ubuntu 64 base box)

## [0.1.1](https://github.com/fgrehm/vagrant-lxc/compare/v0.1.0...v0.1.1) (March 29, 2013)

  - Removed support for development under Vagrant < 1.1
  - Removed rsync from base quantal64 box to speed up containers creation [#40](https://github.com/fgrehm/vagrant-lxc/issues/40)
  - Containers are now named after project's root dir [#14](https://github.com/fgrehm/vagrant-lxc/issues/14)
  - Skip Vagrant's built in SSH redirect
  - Allow setting rootfs from Vagrantfile [#30](https://github.com/fgrehm/vagrant-lxc/issues/30)

## [0.1.0](https://github.com/fgrehm/vagrant-lxc/compare/v0.0.3...v0.1.0) (March 27, 2013)

  - Support for chef added to base quantal64 box
  - Puppet upgraded to 3.1.1 on base quantal64 box
  - Port forwarding support added [#6](https://github.com/fgrehm/vagrant-lxc/issues/6)

## Previous

The changelog began with version 0.1.0 so any changes prior to that
can be seen by checking the tagged releases and reading git commit
messages.
