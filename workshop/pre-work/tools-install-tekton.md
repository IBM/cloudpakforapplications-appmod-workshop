## Install Tekton CLI

Run the commands below to install `tkn` the Tekton CLI that we will be using in this lab

```console
curl -LO https://github.com/tektoncd/cli/releases/download/v0.9.0/tkn_0.9.0_Linux_x86_64.tar.gz
```
```console
mkdir ~/tknbin
```

```console
tar xvzf tkn_0.9.0_Linux_x86_64.tar.gz -C ~/tknbin tkn
```

```console
echo 'export PATH=$HOME/tknbin:$PATH' > .bash_profile
```

```console
source .bash_profile
```

```console
tkn version
```