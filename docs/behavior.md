# Categorization

`nix-gui`{.verbatim} categorizes different components of nixos into
system settings based on the options, but recategorized based on
frequency of use.

-   Packages: environment.systemPackages
-   Users: users
-   Interface: xserver
-   Fonts: fonts
-   ... (TODO)
-   All Configurations: (nixpkgs.config basic tree layout)

## Custom Categorization

There is a lot of noise in \<nixpkgs>.config. So not only will we want
to have the option to prioritize certain settings, but we will also want
to be able to move things around and create our own categories, for
example

-   environment.systemPackages is now its own category
-   networking.networkmanager, hardware.bluetooth, are all within their
    own new tree

## Easy Settings

Rather than relying on the user providing sane settings, we want to
allow a sane set of defaults that can be refined. This may be considered
a project unto itself, or an improvement in nixos in general. NUR and
nix-home have some good examples.

Example of unnecessarily complex setting:

hardware.bluetooth.settings.General.Enable =
\"Source,Sink,Media,Socket\";

## Safety

There must be a system which identifies options or option sets which are
risky to change

# Priority Ordering

Configurations are ordered and categorized with multiple precedents. The
top ranking priority order is used first if available, otherwise the
following is used:

-   `nix_gui`{.verbatim} includes a hardcoded priority / grouping
    configuration for the most obvious settings
-   Github provides hints at the settings which are most frequently used
    (scraping can be done with <https://github.com/shobrook/git-pull>)
-   For options which aren\'t hardcoded or frequently used, alphabetical
    ordering is utilized.

### Hardcoded

Packages are configured in two ways:

-   install: add to environment.systemPackages
-   configure: update the related configuration
    -   this part is much more difficult, we must determine where the
        cfg for the installed package lives, for example [in
        networkmanager it lives in
        networking.networkmanager](https://github.com/NixOS/nixpkgs/blob/8284fc30c84ea47e63209d1a892aca1dfcd6bdf3/nixos/modules/services/networking/networkmanager.nix#L6).
    -   configure

At some point it may be worthwhile to even include icons.

### From Github

A crawl of github will be used to determine the options which are most
frequently defined. The cached rate of option use will be provided to
users. Options which are most frequently used will be listed first.

Thankfully many users have included their system configuration files
making this possible.

### Fallback

Alphabetical.
