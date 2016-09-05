# Using multiple versions of docker 

In case you run into the situation where your local version of the docker client and the API version of the docker server do not match, you might need to install another version of the docker client locally on your machine.
[Docker Version Manager](https://github.com/getcarina/dvm) which is similar to the nodejs version manager [nvm](https://github.com/creationix/nvm) allows you to do exactly this.

If you are on Mac OSX and have homebrew installed, installation of dvm is pretty easy:

```
$ brew update && brew install dvm
```

Then to install a specific version and use it:

```
dvm install 1.10.0 && dvm use 1.10.0
```
