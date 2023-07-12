# Building the code

you can build the code with `make` if you run into dependency issues you can try

`sudo go env -w GOPROXY=direct` 

`sudo go mod download`

`sudo make`

# How to run kubernetes locally


https://github.com/kubernetes/community/blob/master/contributors/devel/development.md for official comprehensive documentation.

https://github.com/kubernetes/community/blob/master/contributors/devel/running-locally.md 

helpful commands for getting setup to run k8s locally and running it for quick testing

You need conatinerd and to configure the cni (along with a couple other thigns I'll pull from k8s docs this is wip), this guide is for running on a linux box

Must install cni to run pods, https://github.com/containerd/containerd/blob/main/script/setup/install-cni

`sudo systemctl stop containerd.service && sudo containerd` on a linux box to run containerd.

Then I usually open another tab and run 

`./hack/local-up-cluster.sh` to spin up a kubernetes cluster quickly with local code.

From there it will output instructions for connecting to kube-apiserver with kubectl and you can begin testing locally.

