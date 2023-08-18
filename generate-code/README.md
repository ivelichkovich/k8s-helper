# Generating Code

Kubernetes has a lot of automatically generated code and documentation. This contains some helpful commands and tips when using these generation scripts.


External APIs in the staging/src/k8s.io/api directory have protobuf files, the user should update types.go while generated.proto, generated.pb.go, types_swagger_doc_generated.go and zz_generated.deepcopy.go should be left to automation to generate.

`./hack/update-codegen.sh` from root of kubernetes to run code generation.

Additionally, the types.go files contain tons of documentation and an openapi spec. When updating docs and apis after running update-codegen run `./hack/update-openapi-spec.sh` 
