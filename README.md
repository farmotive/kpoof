The purpose of kpoof is to provide an opinionated port-forwarder into a kubernetes container.  Traditionally, if one wanted to port-forward into a kubernetes container, one had to `kubectl get pods --namespace foo`, visually identify the pod of interest, copy that pod to the buffer, and then `kubectl --namespace foo port-forward <paste_buffer> <local-port>:<remote-port>` to port-forward into the pod.  This simple utility aims to provide a namespace-specific pod selector for quick port-forwarding.  The default behavior of kpoof is to port-forward all exposed ports.  Because \*nix denies binding to ports below 1001, kpoof assigns a port of `n`+50000, where `n` is a sub-1001 port.

# kpoof

[![asciicast](https://asciinema.org/a/142452.png)](https://asciinema.org/a/142452)

```sh
kpoof(1)

NAME
    kpoof - Quick k8s pod port-forward utility.

REQUIRES
    kubectl(1)

SYNOPSIS
    kpoof [OPTIONS]

  DESCRIPTION
      ${SCRIPT} is a quick kubernetes (k8s) utility to port-forward a pod to localhost (127.0.0.1). ${SCRIPT} prompts for:
        - <NAMESPACE> (defaults to current ns. See kubens(1))
        - <POD> (defaults to "1")
      ENTER to use defaults.

  OPTIONS
      -h, --help
          Show this help message
      -d, --daemon
          Run kpoof as a daemon
      -k, --killd
          Kills a kpoof command daemon, if running
      -a, --killd-all
          Kills all running kpoof command daemons defined in $HOME/.kpoof/kpoofd

SEE ALSO
    kubectx(1), kubens(1), kex(1)
```

### USAGE

```sh
$ kpoof
Namespace? (default qux):
    1 qux
    2 quux
    3 quuz
    4 corge
    5 grault
    6 garply
    7 waldo
    8 fred
    9 plugh
    10 xyzzy
    11 thud
4
Pod number? (default 1):
    1 foo-drupal
    2 bar-mariadb
    3 baz-alpine
2
Forwarding from 127.0.0.1:3306 -> 3306
```

## Installation

**For macOS:**

Use the [Homebrew](https://brew.sh/) package manager:
```sh
brew tap farmotive/k8s
brew install kpoof
```
**NOTE:** If using gcloud sdk to manage the installation and versioning of `kubectl`, install with the `--without-kubernetes-cli` flag to omit the brew dependency:
```sh
brew install kpoof --without-kubernetes-cli
```

See [farmotive homebrew k8s install section](https://github.com/farmotive/homebrew-k8s#install) for more options.

**Other platforms:**

- Download the `kpoof` script
- Add it somewhere in your PATH
- Make it executable (`chmod +x`)

-----

Disclaimer: This is not an official Google product.

Thanks to [ahmetb](https://github.com/ahmetb) for the inspiration!
