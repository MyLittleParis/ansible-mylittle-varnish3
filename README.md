Ansible Role: Varnish3.0
=========

Installs Varnish on Debian/Ubuntu Linux servers.

This role installs and configures the 3.0 version of Varnish from the Varnish repositories via apt (on Debian-based systems) . You will likely need to do extra setup work after this role has installed Varnish, like adding your own [config].vcl file inside /etc/varnish/, describing the location and options to use for your particular caching rules.

Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

    varnish_version: "3.0.7"

Set the varnish version to install.


    varnish_listening_port: "80"

Set the listening varnish port.

    varnish_source_path: "/opt/varnish-src"

Set the varnish source path. Will be used to download varnish source for the compilation of vmods.

    varnish_systemd_path: "/etc/systemd/system/varnish.service.d"

Path to create for handle varnish startup options with systemd managed linux.

    varnish_apt_keys: "https://repo.varnish-cache.org/GPG-key.txt"

Official varnish GPG keys used for trust varnish repositories.

    varnish_apt_repositories:
      - "deb https://repo.varnish-cache.org/debian/ jessie varnish-3.0"
      - "deb-src https://repo.varnish-cache.org/debian/ jessie varnish-3.0"

Add here all repositories you need to download your varnish version.

    varnish_vmods_paths:
      old: "/usr/local/lib/varnish/vmods"
      new: "/usr/lib/varnish/vmods"

Paths to vmods library. `old` is used here to create symbolic link to `new` path.

    varnish_vmods: 
      - name: "libvmod_ipcast"
        url: "https://github.com/lkarsten/libvmod-ipcast.git"
        version: "master"
      - name: "libvmod_header"
        url: "https://github.com/varnish/libvmod-header.git"
        version: "3.0"

List all your vmods git repositories here. 

    varnish_apt_packages:
      - curl
      - dpkg-dev
      - git
      - make
      - automake
      - libncurses5-dev
      - libtool
      - pkg-config

A list of packages to install before executing any steps.

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      become: yes
      roles:
         - { role: Melvin-mlp.ansible-mylittle-varnish3 }

License
-------

BSD

Author Information
------------------

This role was created in 2017 by Melvin Dias, author of nothing.
=======
