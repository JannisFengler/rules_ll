<!-- Generated with Stardoc: http://skydoc.bazel.build -->

# `//ll:llvm_project_deps.bzl`

Convenience variable to depend on LLVM and Clang. Useful when building something
that would normally require forking the llvm-project repo. Put this in the
`llvm_project_deps` attribute to make them available to a target.