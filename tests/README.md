# Quick Start Test Commands

official testing guide https://github.com/kubernetes/community/blob/master/contributors/devel/sig-testing/testing.md


For `Unit Tests` you can run from your IDE or run `make test WHAT=./pkg/kubelet`.

For `Integration Tests` you can use a command similar to `make test-integration WHAT=./test/integration/apiserver/admissionwebhook GOFLAGS="-v" KUBE_TEST_ARGS="-run ^TestWebhookExclusionRules$"` then you can remove KUBE_TEST_ARGS to not specify individual tests or even remove WHAT to run the entire test suite.

# E2E Tests

There are several ways to run E2E tests. This shows how to run them locally with kind.

Install gsutil: https://cloud.google.com/storage/docs/gsutil_install#linux
Install kind: https://kind.sigs.k8s.io/docs/user/quick-start/
Install kubetest2: https://github.com/kubernetes-sigs/kubetest2

Now create a kind cluster, reference kind documentation for additional args and configurations but for a basic cluster just run
`kind create cluster`

now you can run kubetest2

`kubetest2 kind -v 10 --test ginkgo -- --focus-regex='AdmissionWebhook' --ginkgo-args="--v"`


