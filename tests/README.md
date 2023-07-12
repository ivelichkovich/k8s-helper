# Quick Start Test Commands

official testing guide https://github.com/kubernetes/community/blob/master/contributors/devel/sig-testing/testing.md


For `Unit Tests` you can run from your IDE or run `make test WHAT=./pkg/kubelet`.

For `Integration Tests` you can use a command similar to `make test-integration WHAT=./test/integration/apiserver/admissionwebhook GOFLAGS="-v" KUBE_TEST_ARGS="-run ^TestWebhookExclusionRules$"` then you can remove KUBE_TEST_ARGS to not specify individual tests or even remove WHAT to run the entire test suite.

# E2E Tests

There are several ways to run E2E tests. This shows how to run them locally with kind.

Install gsutil: https://cloud.google.com/storage/docs/gsutil_install#linux # only needed if not running local tests
Install kind: https://kind.sigs.k8s.io/docs/user/quick-start/
Install kubetest2: https://github.com/kubernetes-sigs/kubetest2

Now create a kind cluster, reference kind documentation for additional args and configurations but for a basic cluster just run
`kind create cluster`

now you can run kubetest2

`kubetest2 kind -v 10 --test ginkgo -- --focus-regex='AdmissionWebhook' --ginkgo-args="--v"`

this will not run the tests you have locally however, so to run them you can use the UseBuiltBinaries flag from the ginkgo runner https://github.com/kubernetes-sigs/kubetest2/blob/master/pkg/testers/ginkgo/ginkgo.go#L39 to point to your binaries after running `make WHAT="test/e2e/e2e.test vendor/github.com/onsi/ginkgo/ginkgo cmd/kubectl"` 

or you can run `make WHAT="test/e2e/e2e.test` and then run `./_output/bin/e2e.test -context kind-kind -ginkgo.focus="AdmissionWebhook" -num-nodes 2` with kubeconfig flags to set the kubeconfig to run your tests. If you don't define the kubeconfig it'll try to use an in-cluster-config and panic.

