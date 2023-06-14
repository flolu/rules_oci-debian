load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

###
# This is required to make Bazel run on macOS
# https://github.com/bazelbuild/platforms/releases
###
http_archive(
    name = "platforms",
    sha256 = "5308fc1d8865406a49427ba24a9ab53087f17f5266a7aabbfc28823f3916e1ca",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/platforms/releases/download/0.0.6/platforms-0.0.6.tar.gz",
        "https://github.com/bazelbuild/platforms/releases/download/0.0.6/platforms-0.0.6.tar.gz",
    ],
)

###
# Setup rules_js
# https://github.com/aspect-build/rules_js/releases
###
http_archive(
    name = "aspect_rules_js",
    sha256 = "2a88d837f8fb7bfe46b1d9f413df9a777ec2973e1f812929b597c1971a3a1da5",
    strip_prefix = "rules_js-1.28.0",
    url = "https://github.com/aspect-build/rules_js/releases/download/v1.28.0/rules_js-v1.28.0.tar.gz",
)

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@rules_nodejs//nodejs:repositories.bzl", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    # https://github.com/bazelbuild/rules_nodejs/blob/stable/nodejs/private/node_versions.bzl
    node_version = "18.13.0",
)

load("@aspect_rules_js//npm:npm_import.bzl", "npm_translate_lock")

npm_translate_lock(
    name = "npm",
    lifecycle_hooks_no_sandbox = False,
    npmrc = "@//:.npmrc",
    pnpm_lock = "//:pnpm-lock.yaml",
    verify_node_modules_ignored = "//:.bazelignore",
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()

###
# Setup rules_ts
# https://github.com/aspect-build/rules_ts/releases
# https://github.com/aspect-build/rules_ts/blob/main/ts/private/versions.bzl
###
http_archive(
    name = "aspect_rules_ts",
    sha256 = "40ab6d3d9cc3259da54fe2f162588aba92244af0f151fbc905dcc8e7b8744296",
    strip_prefix = "rules_ts-1.4.2",
    url = "https://github.com/aspect-build/rules_ts/releases/download/v1.4.2/rules_ts-v1.4.2.tar.gz",
)

load("@aspect_rules_ts//ts:repositories.bzl", "rules_ts_dependencies")

rules_ts_dependencies(ts_version_from = "//:package.json")

###
# Setup rules_pkg
# https://github.com/bazelbuild/rules_pkg/releases
###
http_archive(
    name = "rules_pkg",
    sha256 = "8f9ee2dc10c1ae514ee599a8b42ed99fa262b757058f65ad3c384289ff70c4b8",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_pkg/releases/download/0.9.1/rules_pkg-0.9.1.tar.gz",
        "https://github.com/bazelbuild/rules_pkg/releases/download/0.9.1/rules_pkg-0.9.1.tar.gz",
    ],
)

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")

rules_pkg_dependencies()

###
# Setup rules_oci
# https://github.com/bazel-contrib/rules_oci/releases
###
http_archive(
    name = "rules_oci",
    sha256 = "db57efd706f01eb3ce771468366baa1614b5b25f4cce99757e2b8d942155b8ec",
    strip_prefix = "rules_oci-1.0.0",
    url = "https://github.com/bazel-contrib/rules_oci/releases/download/v1.0.0/rules_oci-v1.0.0.tar.gz",
)

load("@rules_oci//oci:dependencies.bzl", "rules_oci_dependencies")

rules_oci_dependencies()

load("@rules_oci//oci:repositories.bzl", "LATEST_CRANE_VERSION", "oci_register_toolchains")

oci_register_toolchains(
    name = "oci",
    crane_version = LATEST_CRANE_VERSION,
)

load("@rules_oci//oci:pull.bzl", "oci_pull")

oci_pull(
    name = "debian",
    digest = "sha256:432f545c6ba13b79e2681f4cc4858788b0ab099fc1cca799cc0fae4687c69070",
    image = "debian",
    platforms = [
        "linux/386",
        "linux/amd64",
        "linux/arm/v5",
        "linux/arm/v7",
        "linux/arm64/v8",
        "linux/mips64le",
        "linux/ppc64le",
        "linux/s390x",
    ],
)
