# Trunk bug

This repo is the minimal steps I required to cause a bug where Trunk can't run gofmt@1.18 in my machine. Note that `main.go` is not properly gofmt-ed for the sake of reproducing the bug.

## The bug only reproduces if there are changes
One thing I've noticed is that `trunk check` will not run anything if there are no changes in `main.go`, so you might want to run something to make it a changed file, ie. `echo "\t" >> main.go` before running trunk check

## Additional information:

```sh
$ go env GOROOT
/usr/local/go

$ go version
go version go1.18 linux/amd64

$ go env GOPATH
# "$HOME" to obscure my home user; company policy
$HOME/go

$ whereis gofmt
/usr/local/go/bin/gofmt

$ echo $SHELL
/bin/zsh
$ zsh --version
zsh 5.8 (x86_64-ubuntu-linux-gnu)

$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 21.10
Release:        21.10
Codename:       impish

$ trunk version
0.9.2-beta
```

## Output file

Whenever I run "trunk check" from zsh, a YAML error file is created in `.trunk/out`:
```yaml
title: Internal trunk error occurred. Please report this issue to us @ https://slack.trunk.io
report:
  - message: Unable to find binary in PATH
    binary: gofmt
    PATH:
      - $HOME/.cache/trunk/linters/go/1.18/bin
  - command: |

    stdin_path: (none)
    run_from: ""
    timeout: 0
    rerun: ""
    exit_status: exited
    exit_code: 0
    stdout: (none)
    stderr: (none)
```

Everything else is as-is on this repo, including `.trunk/trunk.yaml`.
