# `rules_ll`

An upstream Clang/LLVM-based Bazel toolchain for modern C++ and heterogeneous
programming.

## ✨ Setup

1. Install the [nix package manager](https://nixos.org/download.html) and enable
   [flakes](https://nixos.wiki/wiki/Flakes).

2. Enter a `rules_ll` development shell:

    ```bash
    nix develop github:eomii/rules_ll
    ```

3. Create a `rules_ll` compatible workspace:

    ```bash
    ll init
    ```

## 🔗 Links

- [Docs](https://ll.eomii.org)
- [Guides](https://ll.eomii.org/guides)
- [Examples](https://github.com/eomii/rules_ll/tree/main/examples)
- [Discord](https://discord.gg/Ax67899n4y)

## 🚀 C++ modules

Use the `interfaces` and `exposed_interfaces` attributes to build C++ modules.
[C++ modules guide](https://ll.eomii.org/guides/modules).

```python
load(
    "@rules_ll//ll:defs.bzl",
    "ll_binary",
    "ll_library",
)

ll_library(
    name = "mymodule",
    srcs = ["mymodule_impl.cpp"],
    exposed_interfaces = {
        "mymodule_interface.cppm": "mymodule",
    },
    compile_flags = ["-std=c++20"],
)

ll_binary(
    name = "main",
    srcs = ["main.cpp"],
    deps = [":mymodule"],
)
```

## 🧹 Clang-Tidy

Build compilation databases to use Clang-Tidy as part of your workflows and CI
pipelines. [Clang-Tidy guide](https://ll.eomii.org/guides/clang_tidy).

```python
load(
   "@rules_ll//ll:defs.bzl",
   "ll_compilation_database",
)

filegroup(
    name = "clang_tidy_config",
    srcs = [".clang-tidy"],
)

ll_compilation_database(
   name = "compile_commands",
   targets = [
      ":my_very_tidy_target",
   ],
   config = ":clang_tidy_config",
)
```

## 😷 Sanitizers

Integrate sanitizers in your builds with the `sanitizer` attribute.
[Sanitizers guide](https://ll.eomii.org/guides/sanitizers).

```python
load(
    "@rules_ll//ll:defs.bzl",
    "ll_binary",
)

ll_binary(
    name = "sanitizer_example",
    srcs = ["totally_didnt_shoot_myself_in_the_foot.cpp"],
    sanitize = ["address"],
)
```

## 🧮 CUDA and HIP

Use CUDA and HIP without any manual setup. [CUDA and HIP guide](https://ll.eomii.org/guides/cuda_and_hip).

```python
load(
    "@rules_ll//ll:defs.bzl",
    "ll_binary",
)

ll_binary(
    name = "cuda_example",
    srcs = ["look_mum_no_cuda_setup.cu"],
    compilation_mode = "cuda_nvptx",  # Or "hip_nvptx".
    compile_flags = [
        "--std=c++20",
        "--offload-arch=sm_70",  # Your GPU model.
    ],
)
```

## 📜 License

Licensed under the Apache 2.0 License with LLVM exceptions.

This repository uses overlays and automated setups for the CUDA toolkit and HIP.
Using `compilation_mode` for heterogeneous toolchains implies acceptance of
their licenses.
