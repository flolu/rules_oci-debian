**Requirements**

- Linux or macOS
- Node.js
- Docker
- pnpm\*
- Bazelisk\*
- Buildifier\*

**Usage**

```
pnpm i
bazel build //app:image_tar
docker load --input $(bazel cquery --output=files //app:image_tar)
docker run -t rules_oci_debian_repro:latest
```

**Error**

```
ERROR: /home/flolu/.cache/bazel/_bazel_flolu/7cbadce41d07a7c855512872c500f8e2/external/debian/BUILD.bazel:1:6: @debian//:debian depends on @debian_linux_amd64//:debian_linux_amd64 in repository @debian_linux_amd64 which failed to fetch. no such package '@debian_linux_amd64//': too many values to unpack (got 3, want 2)
```

> But it works fine with the [pull.bzl](pull.bzl) helper!
