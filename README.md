# base

Install and configure basic system tools.


## Requirements

This role requires the ```kewlfft.aur``` role and the ```community.general``` collection.

Root access is also required, so either run it in a playbook with a global ```become: true```, or invoke the role in
your playbook like:

    - hosts: all
      roles:
        - role: marcstraube.base
          become: true


## Role variables

Available variables are listed below, along with default values (see ```defaults/main.yml```):

    base_enable_multilib: true

Whether to enable the multilib repository. This is needed for 32-bit support.

    base_custom_repositories: []

List of custom repositories. You can add them like this:

    base_custom_repositories:
      - name: 'alerque'
        server: 'https://arch.alerque.com/$arch'
        key_id: '63CC496475267693'

You can find a list of custom repositories at https://wiki.archlinux.org/index.php/unofficial_user_repositories

    base_mirrors_countries: []

List of countries for the pacman mirrorlist

    base_mirrors_sort: 'rate'

Mirror sorting mechanism for Reflector. Possible values are ```age```, ```rate```, ```country```, ```score``` or ```delay```.

    aur_build_user: 'aur_builder'

User to run the AUR helper as.

The aur_build_user has to execute ```pacman``` without password, for which the sudoers file
```/etc/sudoers.d/11-aur_builder``` will be created.

If you use the provided default value ```aur_builder```, a system user with this name will be created. If you provide
another username, you have to make sure that this user already exists, is a member of the ```wheel``` group and is
allowed to run pacman with password-less sudo.

The ```aur_build_user``` variable is used in all my other roles that build packages from the AUR.

    base_aur_helper: 'paru'

AUR helper to be installed. Possible values are ```paru```, ```yay```, ```pacaur```, ```trizen``` or ```pikaur```.

    base_aur_packager: ''
    base_aur_gpg_key: ''

Packager settings.

    base_aur_dev_tools: true

Wheter to install AUR developer tools. These come handy, if you maintain your own packages in the AUR.

    base_kernel: 'linux'

Possible values: ```linux```, ```linux-hardened```, ```linux-lts``` or ```linux-zen```.

    base_packages:
      - 'base'
      - 'bash-completion'
      - 'hdparm'
      - 'htop'
      - 'iproute2'
      - 'man-db'
      - 'man-pages'
      - 'mlocate'
      - 'multitail'
      - 'neovim'
      - 'pkgfile'
      - 'texinfo'
      - 'tmux'
      - 'wget'
      - 'vifm'

List of basic system packages to be installed.

    base_aur_packages:
    - 'ancient-packages'
    - 'aurvote'
    - 'nvimpager-git'

List of basic system packages to be installed from the AUR.


## Example Playbook

    - hosts: 'all'
      become: true
      roles:
        - 'marcstraube.base'


## License

GPLv3
