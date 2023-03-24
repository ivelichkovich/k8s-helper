# Kubernetes Imports

### Import Ordering

Kuberentes import ordering should be zero-path, space, other deps, space, k8s.io deps.

Example:

```
	"errors"
	"fmt"
	"reflect"
	"time"

	"github.com/google/cel-go/interpreter"

	admissionv1 "k8s.io/api/admission/v1"
	authenticationv1 "k8s.io/api/authentication/v1"
	metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
	"k8s.io/apimachinery/pkg/apis/meta/v1/unstructured"
	"k8s.io/apimachinery/pkg/runtime"
	"k8s.io/apiserver/pkg/admission"
```

You can automatically format the imports with 

### goimports command

`goimports -w -local k8s.io <file>`

### vscode

In vscode, you can just set the local formatting flag for gopls in the workspace: "gopls": {"formatting.local": "k8s.io"}

### GoLand/Other git pre-commit script

I wasn't able to figure out how to force goland to use the kubernetes goimports so instead I made a pre-commit scripts for my git configuration.

Just add this file as `pre-commit` in `.git/hooks` and make sure it's executable `chmod +x pre-commit` and now everytime you commit, the changed files will have `goimports -w -local k8s.io <file>` ran against them and then they will be staged for commit. (note this script specifically will also git add on all changed files)


```
#!/bin/bash

#pre commit hook that runs custom import ordering for kubernetes
#custom import ordering is zero-path deps, then space, then other deps, then space, then k8s.io deps
for changedFile in $(git diff --name-only --cached --relative)
do
	goimports -w -local k8s.io $changedFile || true
	go fmt $changedFile || true
	git add $changedFile
done
```