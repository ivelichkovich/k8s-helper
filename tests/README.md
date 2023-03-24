# Quick Start Test Commands

official testing guide https://github.com/kubernetes/community/blob/master/contributors/devel/sig-testing/testing.md


For `Unit Tests` you can run from your IDE or run `make test WHAT=./pkg/kubelet`.

For `Integration Tests` you can use a command similar to `make test-integration WHAT=./test/integration/apiserver/admissionwebhook GOFLAGS="-v" KUBE_TEST_ARGS="-run ^TestWebhookExclusionRules$"` then you can remove KUBE_TEST_ARGS to not specify individual tests or even remove WHAT to run the entire test suite.