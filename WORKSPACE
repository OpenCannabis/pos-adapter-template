
workspace(
    name = "ocp_adapter",
)

load(
    "@bazel_tools//tools/build_defs/repo:http.bzl",
    "http_archive",
    "http_file",
)

load(
    "@bazel_tools//tools/build_defs/repo:git.bzl",
    "git_repository",
)


http_archive(
    name = "opencannabis",
    sha256 = None,
    strip_prefix = "specification-ee04e48375ad17d2d6111b8aaf871a1bac1055f9",
    urls = ["https://github.com/CookiesCo/Specification/archive/ee04e48375ad17d2d6111b8aaf871a1bac1055f9.tar.gz"],
)

http_archive(
    name = "com_google_protobuf",
    sha256 = "c6003e1d2e7fefa78a3039f19f383b4f3a61e81be8c19356f85b6461998ad3db",
    strip_prefix = "protobuf-%s" % PROTOBUF_VERSION,
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v%s.tar.gz" % PROTOBUF_VERSION],
)

http_archive(
    name = "com_google_googleapis",
    sha256 = "0424d63c6718183a06f0219e09de7d400a2bd5ca570e1822be4f73f59f9b5a56",
    strip_prefix = "googleapis-882e6d69a30e4bde445dd33c710f1235b81270c7",
    urls = ["https://github.com/googleapis/googleapis/archive/882e6d69a30e4bde445dd33c710f1235b81270c7.tar.gz"],
)

http_archive(
    name = "com_github_grpc_grpc",
    strip_prefix = "grpc-%s" % GRPC_VERSION,
    sha256 = "df488fc6ecdc51bfa026fedb552f23b7cd31ce87d4aa38f676d814903f240062",
    urls = ["https://github.com/grpc/grpc/archive/v%s.zip" % GRPC_VERSION],
)

http_archive(
    name = "io_grpc_proto",
    sha256 = "f081eba5884bf09051d27664aede4fc22bbaa77da477735d745bcef17bd088f1",
    strip_prefix = "grpc-proto-ec886024c2f7b7f597ba89d5b7d60c3f94627b17",
    urls = ["https://github.com/grpc/grpc-proto/archive/ec886024c2f7b7f597ba89d5b7d60c3f94627b17.tar.gz"],
)

http_archive(
    name = "io_grpc_java",
    sha256 = "85927f857e0b3ad5c4e51c2e6d29213d3e0319f20784aa2113552f71311ba74c",
    strip_prefix = "grpc-java-%s" % GRPC_VERSION,
    urls = ["https://github.com/grpc/grpc-java/archive/v%s.tar.gz" % GRPC_VERSION],
)

# Python rules should go early in the dependencies list, otherwise a wrong
# version of the library will be selected as a transitive dependency of gRPC.
http_archive(
    name = "rules_python",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.3.0/rules_python-0.3.0.tar.gz",
    sha256 = "934c9ceb552e84577b0faf1e5a2f0450314985b4d8712b2b70717dc679fdc01b",
)

load(
    "@com_google_protobuf//:protobuf_deps.bzl",
    "protobuf_deps",
)

protobuf_deps()

http_archive(
    name = "rules_proto",
    sha256 = "602e7161d9195e50246177e7c55b2f39950a9cf7366f74ed5f22fd45750cd208",
    strip_prefix = "rules_proto-97d8af4dc474595af3900dd85cb3a29ad28cc313",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
        "https://github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
    ],
)


load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()

rules_proto_toolchains()

#
# Buf
#

RULES_BUF_VERSION = "7e55fac95a13c2fd126201dc1aacc5a2af04c356"
RULES_BUF_FINGERPRINT = "736f446b4fcf929e4fffdc73779672fd25873ddaa2693f081ea35b1f342c1fd6"

(local_repository(
    name = "rules_buf",
    path = "/Users/sam.g/Workspace/rules_buf",
) if LOCAL else http_archive(
    name = "rules_buf",
    urls = ["https://github.com/sgammon/rules_buf/archive/%s.tar.gz" % RULES_BUF_VERSION],
    strip_prefix = "rules_buf-%s" % RULES_BUF_VERSION,
    sha256 = RULES_BUF_FINGERPRINT,
))


#
# Java
#

RULES_JVM_EXTERNAL_TAG = "4.1"
RULES_JVM_EXTERNAL_SHA = "f36441aa876c4f6427bfb2d1f2d723b48e9d930b62662bf723ddfb8fc80f0140"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "1f4e59843b61981a96835dc4ac377ad4da9f8c334ebe5e0bb3f58f80c09735f4",
    strip_prefix = "rules_docker-0.19.0",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.19.0/rules_docker-v0.19.0.tar.gz"],
)

load("@io_bazel_rules_docker//repositories:repositories.bzl", container_repositories = "repositories")
load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_repositories()
container_deps()

## Stardoc
load("@io_bazel_stardoc//:setup.bzl", "stardoc_repositories")
stardoc_repositories()


## Containers
load("@io_bazel_rules_docker//container:container.bzl", "container_pull")

