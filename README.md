# Bazel build rules for [jemalloc](https://github.com/jemalloc/jemalloc)

Follows a "repos/deps" pattern (in order to help with recursive dependencies). To use:

1. Copy `bazel/repos.bzl` into your repository at `3rdparty/bazel-rules-jemalloc/repos.bzl` as well.

2. Copy all of the directories from `3rdparty` that you ***don't*** already have in ***your*** repository's `3rdparty` directory.

3. Either ... add the following to your `WORKSPACE` (or `WORKSPACE.bazel`):

```bazel
load("//3rdparty/bazel-rules-jemalloc:repos.bzl", jemalloc_repos="repos")
jemalloc_repos()

load("@com_github_3rdparty_bazel_rules_jemalloc//bazel:deps.bzl", jemalloc_deps="deps")
jemalloc_deps()
```

Or ... to simplify others depending on ***your*** repository, add the following to your `repos.bzl`:

```bazel
load("//3rdparty/bazel-rules-jemalloc:repos.bzl", jemalloc_repos="repos")

def repos():
    jemalloc_repos()
```

And the following to your `deps.bzl`:

```bazel
load("@com_github_3rdparty_bazel_rules_jemalloc//bazel:deps.bzl", jemalloc_deps="deps")

def deps():
    jemalloc_deps()
```

4. You can then use `@com_github_jemalloc_jemalloc//:jemalloc` in your target's `deps`.

5. Repeat the steps starting at (1) at the desired version of this repository that you want to use:

| jemalloc | Copy `bazel/repos.bzl` from: |
| :---: | :--------------------------: |
| 1.42.0 | [16758d8](https://github.com/3rdparty/bazel-rules-jemalloc/tree/16758d840b7abf529943e78bc7afa2a7e5381dc0) |
