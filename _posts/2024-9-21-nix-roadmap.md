---
layout: post
title: Nix Learning Roadmap
tags: nix devops
---



> Nix can be used to make `reproducible development environemnts`, which means you can use any program packaged wit hnix while don't have to install them permanently.



Learn the basics of the Nix language.
Play around with the Nix REPL.
Create your first flake, utils, and libs.
Use nix as a package manager first.
Learn how to solve your upstream Linux issues.
Move slowly towards NixOS.


# Nix Language Basics

**General Rule**

- lazy evaluation, which means computes values when needed. (try to prepend `:p` in nix repl.)

- pure expression: declaring data and transform it with functions.

- values:
  - primitives
    - string
      - interpolation
      - file system path
      - lookup path: <nixpkgs> (try to avoid, since it's impurities)
        - Whenever a file system path is used in string interpolation, the contents of that file are copied to a special location in the file system, the Nix store, as a side effect.
        - `/nix/store/<hash>-<name>`
      - indented string '' ''
  - list
  - attribute set
  - function

- assign names to values:
  - attribute set
  - let expression
    - order of assignment does not matter.
    - with

- `;` is used to delimit expressons. last expresson should omit it.

- inherit

- string interpolation: `${...}`, only works for string values.

- funciton
  - only takes on argument.
  - argument and function body are separated by `:`.
  - default arguments: `let f = {a, b ? 0}: a + b; in f {a = 1;}`
  - additional arguments `let f = {a, b, ...}: a + b; in f { a = 1; b = 2; c = 3;}`
  - @ pattern: {a, b, ...}@args: a + b + args.c

  **builtins lib**

  - primitive operations (primops)

  - `import` is available at top level.
    - a classic pattern is to apply argument to the imported function: `import ./file.nix 1`

  - fetchers: Files to be used as build inputs do not have to come from the file system.
    - builtins.fetchurl
    - builtins.fetchTarball
    - builtins.fetchGit
    - builtins.fetchClosure
    - These functions evaluate to a file system path in the Nix store.

  **pkgs.lib**


  **Derivations**

  core of both nix and nix language.

  - The Nix language is used to describe derivations.
  - Nix runs derivations to produce build results.
  - Build results can in turn be used as inputs for other derivations.
  - compared to impore `derivation` function, `stdenv.mkDerication` is more common.
  - The result of above functions is an attr set with certian structure and a special property: when user in string interpolation, it will evelautes to the nix store path of the build result.

  ??? stop at worked examples. https://nix.dev/tutorials/nix-language

  - The Nix ecosystem and code style is driven by conventions. `nix pills` give introdution regarding derivations.

  **nix pills**

  - derivatins/packages are stored in the nox store as follows: /nix/store/hash-name

  - Since Nix derivations are immutable, upgrading a library like glibc means recompiling all applications, because the glibc path to the Nix store has been hardcoded.

  - A derivation from a Nix language view point is simply a set, with some attributes.
    - name 
    - system
    - builder -> The builder will not inherit any variable from your running shell, otherwise builds would suffer from non-determinism.
    - `derivation` function: It takes as input an attribute set, the attributes of which specify the inputs to the process. It outputs an attribute set, and produces a store derivation as a side effect of evaluation.

    - `.drv` file is the specification of how to build the derivation, without all the nix language fuzz.

    - when the derivation is buil, nix separate:
      - instantiate: when nix expression is parsed, a drv set is returned, since nix wil lcreate .drv files, so we konow out paths beforehand.
      - .drv is built, dependencies are built first.

    - nix derivation show /nix/store/i76pr1cz0za3i9r6xq518bqqvd2raspw-foo.drv
    -  Nix automatically copies files or directories needed for the build into the store to ensure that they are not changed during the build process and that the deployment is stateless and independent of the building machine.

    > The trick: every attribute in the set passed to derivation will be converted to a string and passed to the builder as an environment variable. This is how the builder gains access to coreutils and gcc: when converted to strings, the derivations evaluate to their output paths, and appending /bin to these leads us to their binaries.

    I'd like to stop here: https://nixos.org/guides/nix-pills/07-working-derivation

    ```
    export PATH="$coreutils/bin:$gcc/bin"
    mkdir $out
    declare -xp
    gcc -o $out/simple $src
    ```

    -`nix-build`does two jobs:
      - nix-instanttiate -> parse and evaluate simple.nix
      - nix-store -r -> realize

    - inherit foo; -> foo = foo;
    - inherit gcc coreutils; -> gcc = gcc; coreutils = coreutils;
    - inherit (pkgs) gcc coreutils; => gcc = pkgs.gcc; coreutils = pkgs.coreutils;
    - This syntax only makes sense inside sets. 

    - //: The // operator is an operator between two sets. The result is the union of the two sets. In case of conflicts between attribute names, the value on the right set is preferred.

    - This function accepts a parameter pkgs, then returns a function which accepts a parameter attrs.

    ```
    pkgs: attrs:
let 
  defaultAttrs = {
    builder = "${pkgs.bash}/bin/bash";
    args = [./builder.sh];
    baseInputs = with pkgs; [
      gnutar
      gzip
      gnumake
      gcc
      coreutils
      gawk
      gnused
      gnugrep
      binutils.bintools
    ];
    buildInputs = [];
    system = builtins.currentSystem;
  };
in
derivation (defaultAttrs // attrs)
    ```

- analogy
  - Analogy: in C you create objects in the heap, and then you compose them inside new objects. Pointers are used to refer to other objects.
  - In Nix you create derivations stored in the nix store, and then you compose them by creating new derivations. Store paths are used to refer to other derivations.

- builder phase:
  - environemnt setup
  - unpack phase
  - change directory phase
  - configure phase -> ./configure
  - build phase -> make
  - install phase -> make install

  - Approaching builds in this way makes packages self-contained, ensuring (apart from data and configuration) that copying the runtime closure onto another machine is sufficient to run the program. 

- nix-shell: The take-away is that nix-shell drops us in a shell with the same (or very similar) environment used to run the builder.

- gargabe-collector: 
  - GC roots


  - callPackage design pattern.

  - override design pattern.

  - nix laziness: https://nixcademy.com/posts/what-you-need-to-know-about-laziness/

  - nixpkgs has its own manual, it's different from nix language itself.

### Language

nix has attrset and lists

Ways to assign name to value:
- attrbute sets
- `let...in...` expressions
- function arguments

**Functions**

- A function always takes exactly one argument.
- Argument and function body are separated by `:`.
  - On its left is the function argument.
  - On its right is the function body.

### What

**Nix Ecosystem**

- nix package manager
  - non-FHS compliant
  - declarative configuration (versus imperative approach)
- nix language
  - like JSON with functions
- NixOS
- nixpgks
  - more than 10000 packages
  - builder functions
    - mkShell
  - utility functions

### How

- To check `nix store` disk usage: `du -hsc /nix/store`.
- To reduce nix store disk uage: `nix-collect-garbage`.
- For the design of nix, same servide will be launched for differernt project. To avoid conflicts, we can assign differernt ports for them. And kill those service on leave `nix shell`.


A samll discovery of rails. Rails will use `PGPORT` env variable, if it's defined, and use that port to connect to psql.

- Here is how to quit on exit shell: https://github.com/legendofmiracles/lila/blob/nix/shell.nix

but above only works on bash. for zsh, I have no clue.



### Flake

A nix package manager feature that encforces a uniform structure for nix projects, pinning versions of dependencies in lock file.

- `nix flake init`: create a flake in the current directory from a template.
- `nix flake show`: show outputs of a flake.
- `nix flake metadata`: show flake metadata.

**Structure**

- description: a string
- inputs: an attrset
- outputs: a function that takes `self` (current flake) and `inputs` as arguments.

```
{
  description = "A very basic flake";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs?ref=nixos-unstable";
    home-manager.url = "github:nix-community/home-manager";
    home-manager.inputs.nixpkgs.follows = "nixkpgs"; /* home-manager will use nixkpgs from above, instead of its own version of nixpkgs. */
  };

  outputs = { self, nixpkgs } : /* self refers to current flake; nixpkgs is a flake from inputs */
  let
    pkgs = nixpkgs.legacyPackages.aarch64.hello;
  in
  {
    /* For nix run */
    packages.aarch64.default = nixpkgs.legacyPackages.aarch64.hello; /* hello is one of ouputs of nixkpgs flake. */
    
    /* For nix develop */
    devShells.aarch64.default = pkgs.mkShell { /* mkShell is a function from nixpkgs outputs. */
      buildInputs = [pkgs.vim];
    }

    /* For NixOS */
    nixosConfigurations.nixos = nixpkgs.lib.nixosSystem {
      modules = [
        ./configuration.nix
        ({ pkgs, ... } : {
          programs.vim.defaultEditor = true;
        })
      ];
    };
  };
}
```


**Commands**

- `nix run`: run a Nix application.
  - outputs.packages."SYSTEM".default
- `nix build`: build a package.
  - outpus.packages."SYSTEM".default
- `nix develop`: run a bash shell that provides the build environment of a derivation.
  - outpus.devShells."SYSTEM".default
- `nixos-rebuild`: build a nixos system.
  - outpus.nixosConfigurations."HOSTNAME"
- `home-manager`: build a home configuration.
  - outputs.homeConfigurations."USERNAME"




**References**:

- [Nix Reference Manual](https://nix.dev/manual/nix/2.18)
- [Nixpkgs Reference Manual](https://nixos.org/manual/nixpkgs/stable/#sec-functions-library)
- [Ultimate Nix Guide](https://www.youtube.com/watch?v=JCeYq72Sko0&t=905s)
- ['nix shell' vs 'nix develop'](https://www.reddit.com/r/NixOS/comments/r15hx4/nix_shell_vs_nix_develop/)


### Overlay

Overlays are Nix functions which accept two arguments, conventionally called `final` and `prev`, returning a set of packages, to customize Nixpkgs. Please check out [this article](https://nixcademy.com/posts/mastering-nixpkgs-overlays-techniques-and-best-practice/) for detail. 



### Nix Flake & Ruby on Rails

[This](https://github.com/the-nix-way/nix-flake-dev-environments/blob/main/ruby-on-rails/flake.nix) is a sample project to set up ROR dev env by flake.



# Nix REPL
--------------------------
https://aldoborrero.com/posts/2022/12/02/learn-how-to-use-the-nix-repl-effectively/

1. Nix Language Basics

2. `nix repl`

```
# Load nixpkgs
:l <nixpkgs> 

# Load whatever flake you want
flake = builtins.getFlake "github:bobvanderlinden/nixpkgs-ruby" 
flake1 = builtins.getFlake "github:numtide/flake-utils" 

json = flake1.lib.eachDefaultSystem(system: { abc = system; })

builtins.toJSON json
# "{\"abc\":{\"aarch64-darwin\":\"aarch64-darwin\",\"aarch64-linux\":\"aarch64-linux\",\"x86_64-darwin\":\"x86_64-darwin\",\"x86_64-linux\":\"x86_64-linux\"}}"

# how to execute a lambda?
```
