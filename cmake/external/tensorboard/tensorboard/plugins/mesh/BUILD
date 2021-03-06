package(default_visibility = ["//tensorboard:internal"])

licenses(["notice"])  # Apache 2.0
exports_files(["LICENSE"])

load("//tensorboard/defs:protos.bzl", "tb_proto_library")

# Public-facing API, included in Pip package.
py_library(
    name = "mesh",
    srcs = ["__init__.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":summary",
    ],
)

py_library(
    name = "metadata",
    srcs = ["metadata.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":protos_all_py_pb2",
        "//tensorboard/compat/proto:protos_all_py_pb2",
    ],
)

py_test(
    name = "metadata_test",
    size = "small",
    srcs = ["metadata_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":metadata",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/util:test_util",
        "@org_pythonhosted_mock",
        "@org_pythonhosted_six",
    ],
)

py_library(
    name = "mesh_plugin",
    srcs = ["mesh_plugin.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":metadata",
        ":protos_all_py_pb2",
        "//tensorboard:expect_numpy_installed",
        "//tensorboard:plugin_util",
        "//tensorboard/backend:http_util",
        "//tensorboard/plugins:base_plugin",
        "//tensorboard/util:tensor_util",
        "@org_pythonhosted_six",
        "@org_pocoo_werkzeug",
    ],
)

py_library(
    name = "test_utils",
    testonly = 1,
    srcs = ["test_utils.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":summary",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/backend:application",
        "//tensorboard/backend/event_processing:event_multiplexer",
        "@org_pocoo_werkzeug",
    ],
)

py_test(
    name = "mesh_plugin_test",
    size = "small",
    srcs = ["mesh_plugin_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":mesh_plugin",
        ":summary",
        ":test_utils",
        "//tensorboard:expect_numpy_installed",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/backend:application",
        "//tensorboard/backend/event_processing:event_multiplexer",
        "//tensorboard/plugins:base_plugin",
        "//tensorboard/util:test_util",
        "@org_pocoo_werkzeug",
        "@org_pythonhosted_six",
        "@org_pythonhosted_mock",
    ],
)

py_library(
    name = "summary",
    srcs = ["summary.py"],
    srcs_version = "PY2AND3",
    visibility = [
        "//visibility:public",
    ],
    deps = [
        ":metadata",
        ":protos_all_py_pb2",
        "//tensorboard/compat:tensorflow",
    ],
)

py_test(
    name = "summary_test",
    size = "small",
    srcs = ["summary_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":summary",
        ":test_utils",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/util:test_util",
    ],
)

tb_proto_library(
    name = "protos_all",
    srcs = ["plugin_data.proto"],
    visibility = ["//visibility:public"],
)

py_library(
    name = "demo_utils",
    srcs = ["demo_utils.py"],
    srcs_version = "PY2AND3",
    visibility = [
        "//visibility:public",
    ],
    deps = [
        "//tensorboard:expect_numpy_installed",
        "//tensorboard/compat:tensorflow",
    ],
)

py_test(
    name = "demo_utils_test",
    size = "small",
    srcs = ["demo_utils_test.py"],
    data = [
        ":test_data",
        "//tensorboard/compat:tensorflow",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":demo_utils",
    ],
)

py_binary(
    name = "mesh_demo",
    srcs = ["mesh_demo.py"],
    srcs_version = "PY2AND3",
    visibility = [
        "//visibility:public",
    ],
    deps = [
        ":demo_utils",
        ":summary",
        "//tensorboard/compat:tensorflow",
    ],
)

filegroup(
    name = "test_data",
    srcs = [
        "test_data/icosphere.ply",
    ],
    visibility = ["//visibility:public"],
)
