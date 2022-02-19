<!-- Generated with Stardoc: http://skydoc.bazel.build -->

# `//ll:init.bzl`

Initializer function which should be called in the `WORKSPACE.bazel` file.


<a id="#initialize_rules_ll"></a>

## initialize_rules_ll

<pre>
initialize_rules_ll(<a href="#initialize_rules_ll-local_crt_path">local_crt_path</a>, <a href="#initialize_rules_ll-llvm_commit">llvm_commit</a>, <a href="#initialize_rules_ll-llvm_sha256">llvm_sha256</a>)
</pre>

Initializes the LLVM repository.

The correct `local_crt_path` is likely something like `/usr/lib64` or
`/usr/x86_64-unknown-linux-gnu`.

`rules_ll` modifies the existing bazel overlay in the LLVM repository. If
the overlay in `rules_ll` breaks because you specified a custom commit, you
can patch `rules_ll` during import e.g. via

```python
http_archive(
    name = "rules_ll",
    sha256 = "<Correct SHA256>",
    urls = [
        "https://github.com/neqochan/rules_ll/archive/<COMMIT_HASH>.zip"
    ],
    patches = [":my_patch.diff"],
    patch_args = ["-p1"],
)
```


**PARAMETERS**


| Name  | Description | Default Value |
| :------------- | :------------- | :------------- |
| <a id="initialize_rules_ll-local_crt_path"></a>local_crt_path |  The path to the directory containing <code>crt1.o</code>, <code>crti.o</code> and <code>crtn.o</code>.   |  none |
| <a id="initialize_rules_ll-llvm_commit"></a>llvm_commit |  The llvm-commit to use for the <code>llvm-project</code> repository.   |  <code>"e7d65fca7ec470469ad3f8e7689b5e563346e4d7"</code> |
| <a id="initialize_rules_ll-llvm_sha256"></a>llvm_sha256 |  The SHA256 for corresponding to <code>llvm_commit</code>. Bazel will print the correct value if this is set to <code>None</code>.   |  <code>"6a7bd0862b27d0d9b5b1c77b1c765dea32a5d9be9f01a8cc53a909e50555ff27"</code> |