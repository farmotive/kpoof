The purpose of kpoof is to provide an opinionated port-forwarder into a kubernetes container.  Traditionally, if one wanted to port-forward into a kubernetes container, one had to `kubectl get pods --namespace foo`, visually identify the pod of interest, copy that pod to the buffer, and then `kubectl --namespace foo port-forward <paste_buffer> <local-port>:<remote-port>` to port-forward into the pod.  This simple utility aims to provide a namespace-specific pod selector for quick port-forwarding.  If the target pod has more than one exposed port, kpoof will port-forward the first exposed port.

# kpoof

```sh
kpoof(1)

NAME
    kpoof - Quick k8s pod port-forward utility.

REQUIRES
    kubectl(1)

SYNOPSIS
    kpoof [OPTIONS]

DESCRIPTION
    kpoof is a quick kubernetes (k8s) utility to port-foward an exposed port of a pod. kpoof prompts for:
    - <NAMESPACE> (defaults to current ns. See kubens(1))
    - <POD> (defaults to "1")
    - <LOCAL_PORT> (defaults to the exposed port of the pod)
  ENTER to use defaults.

OPTIONS
    -h, --help
        Show this help message

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
Note: *nix ports below 1000 are denied, i.e., use '8080' if the pod is exposing
80 or 443. Local port number? (defaults to 3306):
3307

Forwarding from 127.0.0.1:3307 -> 3306
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
