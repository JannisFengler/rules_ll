# `//ll:defs.bzl`

These are the rules that should be imported in `BUILD.bazel` files.

To load e.g. the `ll_binary` rule:

```python
load("@rules_ll//ll:defs.bzl", "ll_binary")
```


<a id="ll_binary"></a>

## ll_binary
<pre>
ll_binary(<a href="#ll_binary-name">name</a>, <a href="#ll_binary-angled_includes">angled_includes</a>, <a href="#ll_binary-compilation_mode">compilation_mode</a>, <a href="#ll_binary-compile_flags">compile_flags</a>, <a href="#ll_binary-data">data</a>, <a href="#ll_binary-defines">defines</a>, <a href="#ll_binary-depends_on_llvm">depends_on_llvm</a>,
          <a href="#ll_binary-deps">deps</a>, <a href="#ll_binary-exposed_angled_includes">exposed_angled_includes</a>, <a href="#ll_binary-exposed_defines">exposed_defines</a>, <a href="#ll_binary-exposed_hdrs">exposed_hdrs</a>, <a href="#ll_binary-exposed_includes">exposed_includes</a>,
          <a href="#ll_binary-exposed_interfaces">exposed_interfaces</a>, <a href="#ll_binary-exposed_relative_angled_includes">exposed_relative_angled_includes</a>, <a href="#ll_binary-exposed_relative_includes">exposed_relative_includes</a>, <a href="#ll_binary-hdrs">hdrs</a>,
          <a href="#ll_binary-includes">includes</a>, <a href="#ll_binary-interfaces">interfaces</a>, <a href="#ll_binary-libraries">libraries</a>, <a href="#ll_binary-link_flags">link_flags</a>, <a href="#ll_binary-relative_angled_includes">relative_angled_includes</a>, <a href="#ll_binary-relative_includes">relative_includes</a>,
          <a href="#ll_binary-sanitize">sanitize</a>, <a href="#ll_binary-srcs">srcs</a>, <a href="#ll_binary-toolchain_configuration">toolchain_configuration</a>)
</pre>

Creates an executable.

Example:

  ```python
  ll_binary(
      srcs = ["my_executable.cpp"],
  )
  ```

**ATTRIBUTES**


| Name  | Description |
| :---- | :---------- |
| <a id="ll_binary-name"></a>`name` | <code><a href="https://bazel.build/docs/build-ref.html#name">Name</a></code>, required.<br><br> A unique name for this target.   |
| <a id="ll_binary-angled_includes"></a>`angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional angled include paths for this target.<br><br>        Per default all inclusions are quoted includes (via <code></code>-iquote<code></code>).         Paths added here are available as angled includes (via <code></code>-I<code></code>).<br><br>        Only used for this target.   |
| <a id="ll_binary-compilation_mode"></a>`compilation_mode` | <code>String</code>, optional, defaults to <code>"cpp"</code>.<br><br> Enables compilation of heterogeneous single source files.<br><br>        WARNING: VERY EXPERIMENTAL.<br><br>        Prefer using this attribute over adding SYCL/HIP/CUDA flags manually in         the <code>"compile_flags"</code> and <code>"link_flags"</code>.<br><br>        See &lt;TODO: GUIDE&gt; for a detailed explanation of how this flag changes         the autogenerated command line arguments/compile passes.<br><br>        <code>"cpp"</code> will treat compilable sources as regular C++.<br><br>        <code>"cuda_nvidia"</code> will treat compilable sources as CUDA kernels.<br><br>        <code>"hip_nvidia"</code> will treat compilable sources as HIP kernels.<br><br>        <code>"omp_cpu"</code> will enable OpenMP CPU support. Equivalent to adding         <code>-fopenmp</code> to <code>compile_flags</code> and <code>@llvm-project//openmp:libomp</code> to         <code>deps</code>.<br><br>        <code>"sycl_cpu"</code> will enable SYCL CPU support using hipSYCL with the OpenMP         backend. Do not use this. It is not fully implemented yet.<br><br>        <code>"sycl_cuda"</code> will enable highly experimental SYCL CUDA support using         hipSYCL. Do not use this. It is not fully implemented yet.<br><br>        <code>"bootstrap"</code> is used for the internal dependencies of the             <code>ll_toolchain</code> such as <code>libcxxabi</code> etc.   |
| <a id="ll_binary-compile_flags"></a>`compile_flags` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional flags for the compiler.<br><br>        A list of strings <code>["-O3", "-std=c++20"]</code> will be appended to the         compile command line arguments as <code>-O3 -std=c++20</code>.<br><br>        Flag pairs like <code>-Xclang -somearg</code> need to be split into separate flags         <code>["-Xclang", "-somearg"]</code>.<br><br>        Only used for this target.   |
| <a id="ll_binary-data"></a>`data` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Additional files made available to the sandboxed actions         executed within this rule. These files are not appended to the default         line arguments, but are part of the inputs to the actions and may be         added to command line arguments manually via the <code>includes</code>,         and <code>compile_flags</code> (for <code>ll_binary also </code>link_flags<code>) attributes.<br><br>        This attribute may be used to make intermediary outputs from non-ll         targets (e.g. from </code>rules_cc<code> or </code>filegroup<code>) available to the rule.   |
| <a id="ll_binary-defines"></a>`defines` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional defines for this target.<br><br>        A list of strings <code>["MYDEFINE_1", "MYDEFINE_2"]</code> will add         <code>-DMYDEFINE_1 -DMYDEFINE_2</code> to the compile command line.<br><br>        Only used for this target.   |
| <a id="ll_binary-depends_on_llvm"></a>`depends_on_llvm` | <code>Boolean</code>, optional, defaults to <code>False</code>.<br><br> Whether this target directly depends on targets from the         <code>llvm-project-overlay</code>.<br><br>        Setting this to <code>True</code> will make the <code>cc_library</code> targets from the LLVM         project overlay avaliable to this target. Compile actions add         <code>-idirafter</code> include paths to <code>clang/include</code> and <code>llvm/include</code> for         Clang/LLVM internal and generated headers so that they are usable         without setting any additional flags.   |
| <a id="ll_binary-deps"></a>`deps` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> The dependencies for this target.<br><br>        Every dependency needs to be an <code>ll_library</code>.   |
| <a id="ll_binary-exposed_angled_includes"></a>`exposed_angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed angled include paths for this target.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_binary-exposed_defines"></a>`exposed_defines` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed defines for this target.<br><br>        These defines will be defined in the compile actions of direct         dependents.   |
| <a id="ll_binary-exposed_hdrs"></a>`exposed_hdrs` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Exposed headers for this target.<br><br>        Exposed headers are available to depending downstream targets. This is         the place to put the public API headers for a library.   |
| <a id="ll_binary-exposed_includes"></a>`exposed_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed include paths for this target.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_binary-exposed_interfaces"></a>`exposed_interfaces` | <code><a href="https://bazel.build/docs/skylark/lib/dict.html">Dictionary: Label -> String</a></code>, optional, defaults to <code>{}</code>.<br><br> Transitive interfaces for this target.<br><br>        Like <code>interfaces</code>, but both the precompiled modules and the compiled         objects derived from files in this attribute are exposed. Files in         this attribute can see BMIs from modules in <code>interfaces</code>. Primary         module interfaces should go here.   |
| <a id="ll_binary-exposed_relative_angled_includes"></a>`exposed_relative_angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed angled include paths, relative to the         original target workspace.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_binary-exposed_relative_includes"></a>`exposed_relative_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed include paths, relative to the original         target workspace.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_binary-hdrs"></a>`hdrs` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Header files for this target.<br><br>        Headers in this attribute will not be exported, i.e. any generated         include paths are only used for this target and the header files are         not made available to downstream targets.<br><br>        When including header files as <code>#include "some/path/myheader.h"</code> their         include paths need to be specified in the <code>includes</code> attribute as well.   |
| <a id="ll_binary-includes"></a>`includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional quoted include paths for this target.<br><br>        When including a header not via <code>#include "header.h"</code>, but via         <code>#include "subdir/header.h"</code>, the include path needs to be added here in         addition to making the header available in the <code>hdrs</code> attribute.<br><br>        Only used for this target.   |
| <a id="ll_binary-interfaces"></a>`interfaces` | <code><a href="https://bazel.build/docs/skylark/lib/dict.html">Dictionary: Label -> String</a></code>, optional, defaults to <code>{}</code>.<br><br> Module interfaces for this target.<br><br>        See [C++ modules](guides/modules) for usage instructions.<br><br>        Internally, interfaces will be precompiled and then compiled to objects         named <code>&lt;filename&gt;.interface.o</code>. This way object files for modules         implemented via separate interfaces and implementations (such as <code>A.cpp</code>         in <code>srcs</code> and <code>A.cppm</code> in <code>interfaces</code>) do not clash.<br><br>        Files in the same <code>interfaces</code> attribute cannot see each other's BMIs.         This means that multiple <code>ll_library</code> targets may be required to build         a module. (For instance, if a module partition is used by other module         partitions.)<br><br>        The BMIs in <code>interfaces</code> are visible to <code>exposed_interfaces</code>. This         way we can often get away with putting all module partitions in         <code>interfaces</code> and the primary module interface in <code>exposed_interfaces</code>.   |
| <a id="ll_binary-libraries"></a>`libraries` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Additional libraries linked to the final executable.<br><br>        Adds these libraries to the command line arguments for the linker.   |
| <a id="ll_binary-link_flags"></a>`link_flags` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional flags for the linker.<br><br>        For <code>ll_binary</code>:         This is the place for adding library search paths and external link         targets.<br><br>        Assuming you have a library <code>/some/path/libmylib.a</code> on your host system,         you can make <code>mylib.a</code> available to the linker by passing         <code>["-L/some/path", "-lmylib"]</code> to this attribute.<br><br>        Prefer using the <code>libraries</code> attribute for library files already present         within the bazel build graph.   |
| <a id="ll_binary-relative_angled_includes"></a>`relative_angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional angled include paths, relative to the target         workspace.<br><br>        This attribute is useful if we require custom include prefix stripping,         but have dynamic paths, such as ones generated by <code></code>bzlmod<code></code>. So instead         of using <code></code>angled_includes = ["external/mydep.someversion/include"]<code></code> we         can use <code></code>relative_angled_includes = ["include"]<code></code>, and the path to the         workspace will be added automatically.<br><br>        Only used for this target.   |
| <a id="ll_binary-relative_includes"></a>`relative_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional quoted include paths, relative to the target         workspace.<br><br>        This attribute is useful if we require custom include prefix stripping,         but have dynamic paths, such as ones generated by <code></code>bzlmod<code></code>. So instead         of using <code></code>includes = ["external/mydep.someversion/include"]<code></code> we can         use <code></code>relative_includes = ["include"]<code></code>, and the path to the workspace         will be added automatically.<br><br>        Only used for this target.   |
| <a id="ll_binary-sanitize"></a>`sanitize` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Enable sanitizers for this target.<br><br>        Some sanitizers come with heavy performance penalties. Many combinations         of multiple enabled sanitizers are invalid. If possible, use only one at         a time.<br><br>        Since sanitizers find issues during runtime, error reports are         nondeterministic and not reproducible at an address level. Run sanitized         executables multiple times and build them with different optimization         levels to maximize coverage.<br><br>        <code>"address"</code>: Enable AddressSanitizer to detect memory errors. Typical             slowdown introduced is 2x. Executables that invoke CUDA-based             kernels, including those created via HIP and SYCL, need to be run             with <code>ASAN_OPTIONS=protect_shadow_gap=0</code>.         <code>"leak"</code>: Enable LeakSanitizer to detect memory leaks. This is already             integrated in AddressSanitizer. Enable LeakSanitizer if you want to             use it in standalone mode. Almost no performance overhead until the             end of the process where leaks are detected.         <code>"memory"</code>: Enable MemorySanitizer to detect uninitialized reads.             Typical slowdown introduced is 3x. Add             <code>"-fsanitize-memory-track-origins=2"</code> to the <code>compile_flags</code>             attribute to track the origins of uninitialized values.         <code>"undefined_behavior"</code>: Enable UndefinedBehaviorSanitizer to detect             undefined behavior. Small performance overhead.         <code>"thread"</code>: Enable ThreadSanitizer to detect data races. Typical             slowdown is 5x-15x. Typical memory overhead is 5x-10x.   |
| <a id="ll_binary-srcs"></a>`srcs` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Compilable source files for this target.<br><br>        Only compilable files and object files         <code>[".ll", ".o", ".S", ".c", ".cl", ".cpp"]</code> are allowed here.<br><br>        Headers should be placed in the <code>hdrs</code> attribute.   |
| <a id="ll_binary-toolchain_configuration"></a>`toolchain_configuration` | <code><a href="https://bazel.build/docs/build-ref.html#labels">Label</a></code>, optional, defaults to <code>//ll:current_ll_toolchain_configuration</code>.<br><br> TODO   |


<a id="ll_compilation_database"></a>

## ll_compilation_database
<pre>
ll_compilation_database(<a href="#ll_compilation_database-name">name</a>, <a href="#ll_compilation_database-config">config</a>, <a href="#ll_compilation_database-exclude">exclude</a>, <a href="#ll_compilation_database-targets">targets</a>)
</pre>

Executable target for building a
[compilation database](https://clang.llvm.org/docs/JSONCompilationDatabase.html)
and running [clang-tidy](https://clang.llvm.org/extra/clang-tidy/) on it.

For a full guide see
[Using `rules_ll` with `clang-tidy`](https://ll.eomii.org/guides/clang_tidy.html).

Examples using this rule are available at
[rules_ll/examples](https://github.com/eomii/rules_ll/tree/main/examples).

**ATTRIBUTES**


| Name  | Description |
| :---- | :---------- |
| <a id="ll_compilation_database-name"></a>`name` | <code><a href="https://bazel.build/docs/build-ref.html#name">Name</a></code>, required.<br><br> A unique name for this target.   |
| <a id="ll_compilation_database-config"></a>`config` | <code><a href="https://bazel.build/docs/build-ref.html#labels">Label</a></code>, required.<br><br> The label of a <code>.clang-tidy</code> configuration file.<br><br>            This file should be at the root of your project directory.   |
| <a id="ll_compilation_database-exclude"></a>`exclude` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Exclude all targets whose path includes one at least one of the             provided strings.   |
| <a id="ll_compilation_database-targets"></a>`targets` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, required.<br><br> The label for which the compilation database should be built.   |


<a id="ll_library"></a>

## ll_library
<pre>
ll_library(<a href="#ll_library-name">name</a>, <a href="#ll_library-angled_includes">angled_includes</a>, <a href="#ll_library-bitcode_libraries">bitcode_libraries</a>, <a href="#ll_library-bitcode_link_flags">bitcode_link_flags</a>, <a href="#ll_library-compilation_mode">compilation_mode</a>,
           <a href="#ll_library-compile_flags">compile_flags</a>, <a href="#ll_library-data">data</a>, <a href="#ll_library-defines">defines</a>, <a href="#ll_library-depends_on_llvm">depends_on_llvm</a>, <a href="#ll_library-deps">deps</a>, <a href="#ll_library-emit">emit</a>, <a href="#ll_library-exposed_angled_includes">exposed_angled_includes</a>,
           <a href="#ll_library-exposed_defines">exposed_defines</a>, <a href="#ll_library-exposed_hdrs">exposed_hdrs</a>, <a href="#ll_library-exposed_includes">exposed_includes</a>, <a href="#ll_library-exposed_interfaces">exposed_interfaces</a>,
           <a href="#ll_library-exposed_relative_angled_includes">exposed_relative_angled_includes</a>, <a href="#ll_library-exposed_relative_includes">exposed_relative_includes</a>, <a href="#ll_library-hdrs">hdrs</a>, <a href="#ll_library-includes">includes</a>, <a href="#ll_library-interfaces">interfaces</a>,
           <a href="#ll_library-relative_angled_includes">relative_angled_includes</a>, <a href="#ll_library-relative_includes">relative_includes</a>, <a href="#ll_library-sanitize">sanitize</a>, <a href="#ll_library-shared_object_link_flags">shared_object_link_flags</a>, <a href="#ll_library-srcs">srcs</a>,
           <a href="#ll_library-toolchain_configuration">toolchain_configuration</a>)
</pre>

Creates a static archive.

Example:

  ```python
  ll_library(
      srcs = ["my_library.cpp"],
  )
  ```

**ATTRIBUTES**


| Name  | Description |
| :---- | :---------- |
| <a id="ll_library-name"></a>`name` | <code><a href="https://bazel.build/docs/build-ref.html#name">Name</a></code>, required.<br><br> A unique name for this target.   |
| <a id="ll_library-angled_includes"></a>`angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional angled include paths for this target.<br><br>        Per default all inclusions are quoted includes (via <code></code>-iquote<code></code>).         Paths added here are available as angled includes (via <code></code>-I<code></code>).<br><br>        Only used for this target.   |
| <a id="ll_library-bitcode_libraries"></a>`bitcode_libraries` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Additional bitcode libraries that should be linked to the         output.<br><br>        Only used if <code>emit</code> includes <code>"bitcode"</code>.   |
| <a id="ll_library-bitcode_link_flags"></a>`bitcode_link_flags` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional flags for the bitcode linker when emitting bitcode.<br><br>        Only Used if <code>emit</code> includes <code>"bitcode"</code>.   |
| <a id="ll_library-compilation_mode"></a>`compilation_mode` | <code>String</code>, optional, defaults to <code>"cpp"</code>.<br><br> Enables compilation of heterogeneous single source files.<br><br>        WARNING: VERY EXPERIMENTAL.<br><br>        Prefer using this attribute over adding SYCL/HIP/CUDA flags manually in         the <code>"compile_flags"</code> and <code>"link_flags"</code>.<br><br>        See &lt;TODO: GUIDE&gt; for a detailed explanation of how this flag changes         the autogenerated command line arguments/compile passes.<br><br>        <code>"cpp"</code> will treat compilable sources as regular C++.<br><br>        <code>"cuda_nvidia"</code> will treat compilable sources as CUDA kernels.<br><br>        <code>"hip_nvidia"</code> will treat compilable sources as HIP kernels.<br><br>        <code>"omp_cpu"</code> will enable OpenMP CPU support. Equivalent to adding         <code>-fopenmp</code> to <code>compile_flags</code> and <code>@llvm-project//openmp:libomp</code> to         <code>deps</code>.<br><br>        <code>"sycl_cpu"</code> will enable SYCL CPU support using hipSYCL with the OpenMP         backend. Do not use this. It is not fully implemented yet.<br><br>        <code>"sycl_cuda"</code> will enable highly experimental SYCL CUDA support using         hipSYCL. Do not use this. It is not fully implemented yet.<br><br>        <code>"bootstrap"</code> is used for the internal dependencies of the             <code>ll_toolchain</code> such as <code>libcxxabi</code> etc.   |
| <a id="ll_library-compile_flags"></a>`compile_flags` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional flags for the compiler.<br><br>        A list of strings <code>["-O3", "-std=c++20"]</code> will be appended to the         compile command line arguments as <code>-O3 -std=c++20</code>.<br><br>        Flag pairs like <code>-Xclang -somearg</code> need to be split into separate flags         <code>["-Xclang", "-somearg"]</code>.<br><br>        Only used for this target.   |
| <a id="ll_library-data"></a>`data` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Additional files made available to the sandboxed actions         executed within this rule. These files are not appended to the default         line arguments, but are part of the inputs to the actions and may be         added to command line arguments manually via the <code>includes</code>,         and <code>compile_flags</code> (for <code>ll_binary also </code>link_flags<code>) attributes.<br><br>        This attribute may be used to make intermediary outputs from non-ll         targets (e.g. from </code>rules_cc<code> or </code>filegroup<code>) available to the rule.   |
| <a id="ll_library-defines"></a>`defines` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional defines for this target.<br><br>        A list of strings <code>["MYDEFINE_1", "MYDEFINE_2"]</code> will add         <code>-DMYDEFINE_1 -DMYDEFINE_2</code> to the compile command line.<br><br>        Only used for this target.   |
| <a id="ll_library-depends_on_llvm"></a>`depends_on_llvm` | <code>Boolean</code>, optional, defaults to <code>False</code>.<br><br> Whether this target directly depends on targets from the         <code>llvm-project-overlay</code>.<br><br>        Setting this to <code>True</code> will make the <code>cc_library</code> targets from the LLVM         project overlay avaliable to this target. Compile actions add         <code>-idirafter</code> include paths to <code>clang/include</code> and <code>llvm/include</code> for         Clang/LLVM internal and generated headers so that they are usable         without setting any additional flags.   |
| <a id="ll_library-deps"></a>`deps` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> The dependencies for this target.<br><br>        Every dependency needs to be an <code>ll_library</code>.   |
| <a id="ll_library-emit"></a>`emit` | <code>List of strings</code>, optional, defaults to <code>["archive"]</code>.<br><br> Sets the output mode. Multiple values may be specified.<br><br>        <code>"archive"</code> invokes the archiver and adds an archive with a <code>.a</code>         extension to the outputs.         <code>"shared_object"</code> invokes the linker and adds a shared object with a         <code>.so</code> extension to the outputs.         <code>"bitcode"</code> invokes the bitcode linker and adds an LLVM bitcode file         with a <code>.bc</code> extension to the outputs.         <code>"objects"</code> adds loose object files to the outputs.   |
| <a id="ll_library-exposed_angled_includes"></a>`exposed_angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed angled include paths for this target.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_library-exposed_defines"></a>`exposed_defines` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed defines for this target.<br><br>        These defines will be defined in the compile actions of direct         dependents.   |
| <a id="ll_library-exposed_hdrs"></a>`exposed_hdrs` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Exposed headers for this target.<br><br>        Exposed headers are available to depending downstream targets. This is         the place to put the public API headers for a library.   |
| <a id="ll_library-exposed_includes"></a>`exposed_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed include paths for this target.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_library-exposed_interfaces"></a>`exposed_interfaces` | <code><a href="https://bazel.build/docs/skylark/lib/dict.html">Dictionary: Label -> String</a></code>, optional, defaults to <code>{}</code>.<br><br> Transitive interfaces for this target.<br><br>        Like <code>interfaces</code>, but both the precompiled modules and the compiled         objects derived from files in this attribute are exposed. Files in         this attribute can see BMIs from modules in <code>interfaces</code>. Primary         module interfaces should go here.   |
| <a id="ll_library-exposed_relative_angled_includes"></a>`exposed_relative_angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed angled include paths, relative to the         original target workspace.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_library-exposed_relative_includes"></a>`exposed_relative_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional exposed include paths, relative to the original         target workspace.<br><br>        Includes in this attribute will be added to the compile command line         arguments for direct dependents.   |
| <a id="ll_library-hdrs"></a>`hdrs` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Header files for this target.<br><br>        Headers in this attribute will not be exported, i.e. any generated         include paths are only used for this target and the header files are         not made available to downstream targets.<br><br>        When including header files as <code>#include "some/path/myheader.h"</code> their         include paths need to be specified in the <code>includes</code> attribute as well.   |
| <a id="ll_library-includes"></a>`includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional quoted include paths for this target.<br><br>        When including a header not via <code>#include "header.h"</code>, but via         <code>#include "subdir/header.h"</code>, the include path needs to be added here in         addition to making the header available in the <code>hdrs</code> attribute.<br><br>        Only used for this target.   |
| <a id="ll_library-interfaces"></a>`interfaces` | <code><a href="https://bazel.build/docs/skylark/lib/dict.html">Dictionary: Label -> String</a></code>, optional, defaults to <code>{}</code>.<br><br> Module interfaces for this target.<br><br>        See [C++ modules](guides/modules) for usage instructions.<br><br>        Internally, interfaces will be precompiled and then compiled to objects         named <code>&lt;filename&gt;.interface.o</code>. This way object files for modules         implemented via separate interfaces and implementations (such as <code>A.cpp</code>         in <code>srcs</code> and <code>A.cppm</code> in <code>interfaces</code>) do not clash.<br><br>        Files in the same <code>interfaces</code> attribute cannot see each other's BMIs.         This means that multiple <code>ll_library</code> targets may be required to build         a module. (For instance, if a module partition is used by other module         partitions.)<br><br>        The BMIs in <code>interfaces</code> are visible to <code>exposed_interfaces</code>. This         way we can often get away with putting all module partitions in         <code>interfaces</code> and the primary module interface in <code>exposed_interfaces</code>.   |
| <a id="ll_library-relative_angled_includes"></a>`relative_angled_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional angled include paths, relative to the target         workspace.<br><br>        This attribute is useful if we require custom include prefix stripping,         but have dynamic paths, such as ones generated by <code></code>bzlmod<code></code>. So instead         of using <code></code>angled_includes = ["external/mydep.someversion/include"]<code></code> we         can use <code></code>relative_angled_includes = ["include"]<code></code>, and the path to the         workspace will be added automatically.<br><br>        Only used for this target.   |
| <a id="ll_library-relative_includes"></a>`relative_includes` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional quoted include paths, relative to the target         workspace.<br><br>        This attribute is useful if we require custom include prefix stripping,         but have dynamic paths, such as ones generated by <code></code>bzlmod<code></code>. So instead         of using <code></code>includes = ["external/mydep.someversion/include"]<code></code> we can         use <code></code>relative_includes = ["include"]<code></code>, and the path to the workspace         will be added automatically.<br><br>        Only used for this target.   |
| <a id="ll_library-sanitize"></a>`sanitize` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Enable sanitizers for this target.<br><br>        Some sanitizers come with heavy performance penalties. Many combinations         of multiple enabled sanitizers are invalid. If possible, use only one at         a time.<br><br>        Since sanitizers find issues during runtime, error reports are         nondeterministic and not reproducible at an address level. Run sanitized         executables multiple times and build them with different optimization         levels to maximize coverage.<br><br>        <code>"address"</code>: Enable AddressSanitizer to detect memory errors. Typical             slowdown introduced is 2x. Executables that invoke CUDA-based             kernels, including those created via HIP and SYCL, need to be run             with <code>ASAN_OPTIONS=protect_shadow_gap=0</code>.         <code>"leak"</code>: Enable LeakSanitizer to detect memory leaks. This is already             integrated in AddressSanitizer. Enable LeakSanitizer if you want to             use it in standalone mode. Almost no performance overhead until the             end of the process where leaks are detected.         <code>"memory"</code>: Enable MemorySanitizer to detect uninitialized reads.             Typical slowdown introduced is 3x. Add             <code>"-fsanitize-memory-track-origins=2"</code> to the <code>compile_flags</code>             attribute to track the origins of uninitialized values.         <code>"undefined_behavior"</code>: Enable UndefinedBehaviorSanitizer to detect             undefined behavior. Small performance overhead.         <code>"thread"</code>: Enable ThreadSanitizer to detect data races. Typical             slowdown is 5x-15x. Typical memory overhead is 5x-10x.   |
| <a id="ll_library-shared_object_link_flags"></a>`shared_object_link_flags` | <code>List of strings</code>, optional, defaults to <code>[]</code>.<br><br> Additional flags for the linker when emitting shared objects.<br><br>        Only used if <code>emit</code> includes <code>"shared_object"</code>.   |
| <a id="ll_library-srcs"></a>`srcs` | <code><a href="https://bazel.build/docs/build-ref.html#labels">List of labels</a></code>, optional, defaults to <code>[]</code>.<br><br> Compilable source files for this target.<br><br>        Only compilable files and object files         <code>[".ll", ".o", ".S", ".c", ".cl", ".cpp"]</code> are allowed here.<br><br>        Headers should be placed in the <code>hdrs</code> attribute.   |
| <a id="ll_library-toolchain_configuration"></a>`toolchain_configuration` | <code><a href="https://bazel.build/docs/build-ref.html#labels">Label</a></code>, optional, defaults to <code>//ll:current_ll_toolchain_configuration</code>.<br><br> TODO   |