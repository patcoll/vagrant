## 0.7.4 (unreleased)



## 0.7.3 (April 19, 2011)

  - Retry all SSH on Net::SSH::Disconnect in case SSH is just restarting. [GH-313]
  - Add NFS shared folder support for Arch linux. [GH-346]
  - Fix issue with unknown terminal type output for sudo commands.
  - Forwarded port protocol can now be set as UDP. [GH-311]
  - Chef server file cache path and file backup path can be configured. [GH-310]
  - Setting hostname should work on Debian now. [GH-307]

## 0.7.2 (February 8, 2011)

  - Update JSON dependency to 1.5.1, which works with Ruby 1.9 on
    Windows.
  - Fix sudo issues on sudo < 1.7.0 (again).
  - Fix race condition in SSH, which specifically manifested itself in
    the chef server provisioner. [GH-295]
  - Change sudo shell to use `bash` (configurable). [GH-301]
  - Can now set mac address of host only network. [GH-294]
  - NFS shared folders with spaces now work properly. [GH-293]
  - Failed SSH commands now show output in error message. [GH-285]

## 0.7.1 (January 28, 2011)

  - Change error output with references to VirtualBox 3.2 to 4.0.
  - Internal SSH through net-ssh now uses `IdentitiesOnly` thanks to
    upstream net-ssh fix.
  - Fix issue causing warnings to show with `forwardx11` enabled for SSH. [GH-279]
  - FreeBSD support for host only networks, NFS, halting, etc. [GH-275]
  - Make SSH commands which use sudo compatible with sudo < 1.7.0. [GH-278]
  - Fix broken puppet server provisioner which called a nonexistent
    method.
  - Default SSH host changed from `localhost` to `127.0.0.1` since
    `localhost` is not always loopback.
  - New `shell` provisioner which simply uploads and executes a script as
    root on the VM.
  - Gentoo host only networking no longer fails if alrady setup. [GH-286]
  - Set the host name of your guest OS with `config.vm.host_name` [GH-273]
  - `vagrant ssh-config` now outputs the configured `config.ssh.host`

## 0.7.0 (January 19, 2011)

  - VirtualBox 4.0 support. Support for VirtualBox 3.2 is _dropped_, since
    the API is so different. Stay with the 0.6.x series if you have VirtualBox
    3.2.x.
  - Puppet server provisioner. [GH-262]
  - Use numeric uid/gid in mounting shared folders to increase portability. [GH-252]
  - HTTP downloading follows redirects. [GH-163]
  - Downloaders have clearer output to note what they're doing.
  - Shared folders with no guest path are not automounted. [GH-184]
  - Boxes downloaded during `vagrant up` reload the Vagrantfile config, which
    fixes a problem with box settings not being properly loaded. [GH-231]
  - `config.ssh.forward_x11` to enable the ForwardX11 SSH option. [GH-255]
  - Vagrant source now has a `contrib` directory where contributions of miscellaneous
    addons for Vagrant will be added.
  - Vagrantfiles are now loaded only once (instead of 4+ times) [GH-238]
  - Ability to move home vagrant dir (~/.vagrant) by setting VAGRANT_HOME
    environmental variable.
  - Removed check and error for the "OSE" version of VirtualBox, since with
    VirtualBox 4 this distinction no longer exists.
  - Ability to specify proxy settings for chef. [GH-169]
  - Helpful error message shown if NFS mounting fails. [GH-135]
  - Gentoo guests now support host only networks. [GH-240]
  - RedHat (CentOS included) guests now support host only networks. [GH-260]
  - New Vagrantfile syntax for enabling and configuring provisioners. This
    change is not backwards compatible. [GH-265]
  - Provisioners are now RVM-friendly, meaning if you installed chef or puppet
    with an RVM managed Ruby, Vagrant now finds then. [GH-254]
  - Changed the unused host only network destroy mechanism to check for
    uselessness after the VM is destroyed. This should result in more accurate
    checks.
  - Networks are no longer disabled upon halt/destroy. With the above
    change, its unnecessary.
  - Puppet supports `module_path` configuration to mount local modules directory
    as a shared folder and configure puppet with it. [GH-270]
  - `ssh-config` now outputs `127.0.0.1` as the host instead of `localhost`.

## 0.6.9 (December 21, 2010)

  - Puppet provisioner. [GH-223]
  - Solaris system configurable to use `sudo`.
  - Solaris system registered, so it can be set with `:solaris`.
  - `vagrant package` include can be a directory name, which will cause the
    contents to be recursively copied into the package. [GH-241]
  - Arbitrary options to puppet binary can be set with `config.puppet.options`. [GH-242]
  - BSD hosts use proper GNU sed syntax for clearing NFS shares. [GH-243]
  - Enumerate VMs in a multi-VM environment in order they were defined. [GH-244]
  - Check for VM boot changed to use `timeout` library, which works better with Windows.
  - Show special error if VirtualBox not detected on 64-bit Windows.
  - Show error to Windows users attempting to use host only networking since
    it doesn't work yet.

## 0.6.8 (November 30, 2010)

  - Network interfaces are now up/down in distinct commands instead of just
    restarting "networking." [GH-192]
  - Add missing translation for chef binary missing. [GH-203]
  - Fix default settings for Opscode platform and comments. [GH-213]
  - Blank client name for chef server now uses FQDN by default, instead of "client" [GH-214]
  - Run list can now be nil, which will cause it to sync with chef server (when
    chef server is enabled). [GH-214]
  - Multiple NFS folders now work on linux. [GH-215]
  - Add translation for state "stuck" which is very rare. [GH-218]
  - virtualbox gem dependency minimum raised to 0.7.6 to verify FFI < 1.0.0 is used.
  - Fix issue where box downloading from `vagrant up` didn't reload the box collection. [GH-229]

## 0.6.7 (November 3, 2010)

  - Added validation to verify that a box is specified.
  - Proper error message when box is not found for `config.vm.box`. [GH-195]
  - Fix output of `vagrant status` with multi-vm to be correct. [GH-196]

## 0.6.6 (October 14, 2010)

  - `vagrant status NAME` works once again. [GH-191]
  - Conditional validation of Vagrantfile so that some commands don't validate. [GH-188]
  - Fix "junk" output for ssh-config. [GH-189]
  - Fix port collision handling with greater than two VMs. [GH-185]
  - Fix potential infinite loop with root path if bad CWD is given to environment.

## 0.6.5 (October 8, 2010)

  - Validations on base MAC address to avoid situation described in GH-166, GH-181
    from ever happening again.
  - Properly load sub-VM configuration on first-pass of config loading. Solves
    a LOT of problems with multi-VM. [GH-166] [GH-181]
  - Configuration now only validates on final Vagrantfile proc, so multi-VM
    validates correctly.
  - A nice error message is given if ".vagrant" is a directory and therefore
    can't be accessed. [GH-172]
  - Fix plugin loading in a Rails 2.3.x project. [GH-176]

## 0.6.4 (October 4, 2010)

  - Default VM name is now properly the parent folder of the working directory
    of the environment.
  - Added method to `TestHelpers` to assist with testing new downloaders.
  - `up --no-provision` works again. This disables provisioning during the
    boot process.
  - Action warden doesn't do recovery process on `SystemExit` exceptions,
    allowing the double ctrl-C to work properly again. [related to GH-166]
  - Initial Vagrantfile is now heavily commented with various available
    options. [GH-171]
  - Box add checks if a box already exists before the download. [GH-170]
  - NFS no longer attempts to clean exports file if VM is not created,
    which was causing a stack trace during recovery. [related to GH-166]
  - Basic validation added for Chef configuration (both solo and server).
  - Top config class is now available in all `Vagrant::Config::Base`
    subclasses, which is useful for config validation.
  - Subcommand help shows proper full command in task listing. [GH-168]
  - SSH gives error message if `ssh` binary is not found. [GH-161]
  - SSH gives proper error message if VM is not running. [GH-167]
  - Fix some issues with undefined constants in command errors.

## 0.6.1, 0.6.2, 0.6.3 (September 27, 2010)

A lot of quick releases which all were to fix issues with Ruby 1.8.7
compatibility.

## 0.6.0 (September 27, 2010)

  - VM name now defaults to the name of the containing folder, plus a timestamp.
    This should make it easier to identify VMs in the VirtualBox GUI.
  - Exposed Vagrant test helpers in `Vagrant::TestHelpers` for plugins to easily
    test themselves against Vagrant environments.
  - **Plugins** have landed. Plugins are simply gems which have a `vagrant_init.rb`
    file somewhere in their load path. Please read the documentation on
    vagrantup.com before attempting to create a plugin (which is very easy)
    for more information on how it all works and also some guidelines.
  - `vagrant package` now takes a `--vagrantfile` option to specify a
    Vagrantfile to package. The `--include` approach for including a Vagrantfile
    no longer works (previously built boxes will continue to work).
  - `vagrant package` has new logic with regards to the `--include` option
    depending on if the file path is relative or absolute (they can be
    intermixed):
      * _Relative_ paths are copied directly into the box, preserving
        their path. So `--include lib/foo` would be in the box as "lib/foo"
      * _Absolute_ paths are simply copied files into the root of the
        box. So `--include /lib/foo` would be in the box as "foo"
  - "vagrant_main" is no longer the default run list. Instead, chef
    run list starts empty. It is up to you to specify all recipes in
    the Vagrantfile now.
  - Fixed various issues with certain action middleware not working if
    the VM was not created.
  - SSH connection is retried 5 times if there is a connection refused.
    Related to GH-140.
  - If `http_proxy` environmental variable is set, it will be used as the proxy
    box adding via http.
  - Remove `config.ssh.password`. It hasn't been used for a few versions
    now and was only kept around to avoid exceptions in Vagrantfiles.
  - Configuration is now validated so improper input can be found in
    Vagrantfiles.
  - Fixed issue with not detecting Vagrantfile at root directory ("/").
  - Vagrant now gives a nice error message if there is a syntax error
    in any Vagrantfile. [GH-154]
  - The format of the ".vagrant" file which stores persisted VMs has
    changed. This is **backwards incompatible**. Will provide an upgrade
    utility prior to 0.6 launch.
  - Every [expected] Vagrant error now exits with a clean error message
    and a unique exit status, and raises a unique exception (if you're
    scripting Vagrant).
  - Added I18n gem dependency for pulling strings into clean YML files.
    Vagrant is now localizable as a side effect! Translations welcome.
  - Fixed issue with "Waiting for cleanup" message appearing twice in
    some cases. [GH-145]
  - Converted CLI to use Thor. As a tradeoff, there are some backwards
    incompatibilities:
      * `vagrant package` - The `--include` flag now separates filenames
        by spaces, instead of by commas. e.g. `vagrant package --include x y z`
      * `vagrant ssh` - If you specify a command to execute using the `--execute`
        flag, you may now only specify one command (before you were able to
        specify an arbitrary amount). e.g. `vagrant ssh -e "echo hello"`
      * `vagrant ssh-config` has become `vagrant ssh_config` due to a limitation
        in Thor.

## 0.5.4 (September 7, 2010)

  - Fix issue with the "exec failed" by running on Tiger as well.
  - Give an error when downloading a box which already exists prior
    to actually downloading the box.

## 0.5.3 (August 23, 2010)

  - Add erubis as a dependency since its rendering of `erb` is sane.
  - Fixed poorly formatted Vagrantfile after `vagrant init`. [GH-142]
  - Fixed NFS not working properly with multiple NFS folders.
  - Fixed chef solo provision to work on Windows. It was expanding a linux
    path which prepended a drive letter onto it.

## 0.5.2 (August 3, 2010)

  - `vagrant up` can be used as a way to resume the VM as well (same as
    `vagrant resume`). [GH-134]
  - Sudo uses "-E" flag to preserve environment for chef provisioners.
    This fixes issues with CentOS. [GH-133]
  - Added "IdentitiesOnly yes" to options when `vagrant ssh` is run to
    avoid "Too Many Authentication Failures" error. [GH-131]
  - Fix regression with `package` not working. [GH-132]
  - Added ability to specify box url in `init`, which populates the
    Vagrantfile with the proper `config.vm.box_url`.

## 0.5.1 (July 31, 2010)

  - Allow specifying cookbook paths which exist only on the VM in `config.chef.cookbooks_path`.
    This is used for specifying cookbook paths when `config.chef.recipe_url` is used. [GH-130]
    See updated chef solo documentation for more information on this.
  - No longer show "Disabling host only networks..." if no host only networks
    are destroyed. Quiets `destroy`, `halt`, etc output a bit.
  - Updated getting started guide to be more up to date and generic. [GH-125]
  - Fixed error with doing a `vagrant up` when no Vagrantfile existed. [GH-128]
  - Fixed NFS erroring when NFS wasn't even enabled if `/etc/exports` doesn't
    exist. [GH-126]
  - Fixed `vagrant resume` to properly resume a suspended VM. [GH-122]
  - Fixed `halt`, `destroy`, `reload` to where they failed if the VM was
    in a saved state. [GH-123]
  - Added `config.chef.recipe_url` which allows you to specify a URL to
    a gzipped tar file for chef solo to download cookbooks. See the
    [chef-solo docs](http://wiki.opscode.com/display/chef/Chef+Solo#ChefSolo-RunningfromaURL) for more information.
    [GH-121]
  - Added `vagrant box repackage` which repackages boxes which have
    been added. This is useful in case you want to redistribute a base
    box you have but may have lost the actual "box" file. [GH-120]

## Previous

The changelog began with version 0.5.1 so any changes prior to that
can be seen by checking the tagged releases and reading git commit
messages.

