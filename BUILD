load(
    "@com_github_mvukov_rules_ros//ros:interfaces.bzl",
    "cc_ros_interface_library",
    "ros_interface_library",
)

ros_interface_library(
    name = "bond_interface",
    srcs = glob([
        "bond/msg/*",
    ]),
    # strip the "_msgs" from final search path.
    # Use this for backwards compatability to avoid changing imports for msgs.
    strip_end = True,
    deps = [
        "@ros_common_msgs//:geometry_msgs",
        "@ros_std_msgs//:std_msgs",
    ],
)

# Defines a C++ library made of auto-generated code from the given messages.
cc_ros_interface_library(
    name = "cc_bond_interface",
    strip_end = True,
    deps = [":bond_interface"],
)

cc_library(
    name = "scmlib",
    hdrs = [
        "smclib/include/smclib/statemap.h",
    ],
    includes = [
        "smclib/include",
    ],
)

cc_library(
    name = "bondcpp",
    srcs = [
        "bondcpp/src/BondSM_sm.cpp",
        "bondcpp/src/bond.cpp",
        "bondcpp/src/timeout.cpp",
    ],
    hdrs = [
        "bondcpp/include/bondcpp/BondSM_sm.h",
        "bondcpp/include/bondcpp/bond.h",
        "bondcpp/include/bondcpp/timeout.h",
    ],
    includes = [
        "bondcpp/include",
    ],
    visibility = [
        "//visibility:public",
    ],
    deps = [
        ":cc_bond_interface",
        ":scmlib",
        "@boost//:uuid",
        "@ros_comm//:roscpp_lib",
    ],
)
