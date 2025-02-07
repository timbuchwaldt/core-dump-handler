# core-dump-client

A CLI for running a core dump session on kubernetes using the zipfile generated by [core-dump-handler](https://github.com/IBM/core-dump-handler) 

## experimental

This tool is still under active development but the core functionality is in place. 
Currently it support nodejs, java or default lldb tools. 

## prerequisites 

1. Ensure [core-dump-handler](https://github.com/IBM/core-dump-handler) is installed on your cluster.

2. Install the cli
    * Download the latest build from releases https://github.com/IBM/core-dump-handler/releases
    Rename it cdcli and place it in a folder that is in your $PATH
    * Or build the client with `cargo install core-dump-client`
    If you don't have rust installed you can get it with [rustup](https://rustup.rs)

3. Ensure your `kubectl` client is logged into the cluster
    kubectl install instructions are [available here](https://kubernetes.io/docs/tasks/tools/#kubectl)
   
## usage

Create a debug environment with 
```
cdcli -c [name-of-zipfile] -i [crashed-image-name]
```
e.g. 
```
cdcli 36c0d272-3295-4474-a16e-00885ba04fed-dump-1631477784-crashing-app-848dc79df4-srqkv-node-8-4.zip quay.io/number9/example-crashing-nodejs-app
```

This will log you into a running container with lldb tools and core file info available to you. 

To start a debug session in the environment run`rundebug.sh` command.

```
./rundebug
```

To inspect the metadata that was saved with crash `ls` will list the folder container your core file and the metadata json.

## demo

[![asciicast](https://asciinema.org/a/438878.svg)](https://asciinema.org/a/438878)
