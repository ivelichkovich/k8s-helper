# TODO: fully document findings and links to k8s docs

helpful commands for getting setup to run k8s locally and running it for quick testing

You need conatinerd and to configure the cni (along with a couple other thigns I'll pull from k8s docs this is wip)

`sudo systemctl stop containerd.service && sudo containerd` on a linux box to run containerd.

Then I usually open another tab and run 

`./hack/local-up-cluster.sh` to spin up a kubernetes cluster quickly with local code.

From there it will output instructions for connecting to kube-apiserver with kubectl and you can begin testing locally.

