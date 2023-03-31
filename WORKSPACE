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
    sha256 = "371c34ae25d72ed4e9c72bd646ed88697ea89d0012ea5ed1860d4804f4dd7056",
    # https://github.com/aspect-build/rules_js/issues/971#issuecomment-1491259017
    strip_prefix = "rules_js-002397780d51735f1a98b362fca7018df31e85ac",
    urls = ["https://github.com/aspect-build/rules_js/archive/002397780d51735f1a98b362fca7018df31e85ac.tar.gz"],
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
    sha256 = "8eb25d1fdafc0836f5778d33fb8eaac37c64176481d67872b54b0a05de5be5c0",
    strip_prefix = "rules_ts-1.3.3",
    url = "https://github.com/aspect-build/rules_ts/releases/download/v1.3.3/rules_ts-v1.3.3.tar.gz",
)

load("@aspect_rules_ts//ts:repositories.bzl", "rules_ts_dependencies")

rules_ts_dependencies(ts_version_from = "//:package.json")

###
# Setup rules_pkg
# https://github.com/bazelbuild/rules_pkg/releases
###
http_archive(
    name = "rules_pkg",
    sha256 = "8c20f74bca25d2d442b327ae26768c02cf3c99e93fad0381f32be9aab1967675",
    urls = ["https://github.com/bazelbuild/rules_pkg/releases/download/0.8.1/rules_pkg-0.8.1.tar.gz"],
)

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")

rules_pkg_dependencies()

###
# Setup rules_oci
# https://github.com/bazel-contrib/rules_oci/releases
###
http_archive(
    name = "rules_oci",
    sha256 = "f6125c9a123a2ac58fb6b13b4b8d4631827db9cfac025f434bbbefbd97953f7c",
    strip_prefix = "rules_oci-0.3.9",
    url = "https://github.com/bazel-contrib/rules_oci/releases/download/v0.3.9/rules_oci-v0.3.9.tar.gz",
)

load("@rules_oci//oci:dependencies.bzl", "rules_oci_dependencies")

rules_oci_dependencies()

load("@rules_oci//oci:repositories.bzl", "LATEST_CRANE_VERSION", "oci_register_toolchains")

oci_register_toolchains(
    name = "oci",
    crane_version = LATEST_CRANE_VERSION,
)

###
# WORKS FINE
###
# load(":pull.bzl", "oci_pull")
# oci_pull(
#     name = "debian",
#     architecture = "amd64",
#     image = "thesayyn/debian:oci",
# )
###

###
# DOESN'T WORK
###
load("@rules_oci//oci:pull.bzl", "oci_pull")

oci_pull(
    name = "debian",
    image = "index.docker.io/library/debian",
    platforms = ["linux/amd64"],
    reproducible = False,
    tag = "latest",
)
###
