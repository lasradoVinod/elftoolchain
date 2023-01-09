licenses(["notice"])

package(default_visibility = ["//visibility:public"])

exports_files(["LICENSE"])

elf_generated_files = [
    "libelf/libelf_convert",
    "libelf/libelf_fsize",
    "libelf/libelf_msize",
]

[genrule(
    name = "gen_%s" % generated_file,
    srcs = [
        "libelf/elf_types.m4",
        "%s.m4" % generated_file,
    ],
    outs = ["%s.c" % generated_file],
    cmd = "m4 " +
          "-D SRCDIR=$$(dirname $(location %s.m4))" % generated_file +
          " $(location %s.m4) " % generated_file +
          "> $@",
) for generated_file in elf_generated_files]

genrule(
    name = "gen_sys_elfdefinitions_h",
    srcs = [
        "common/sys/elfconstants.m4",
        "common/sys/elfdefinitions.m4",
    ],
    outs = ["common/sys/elfdefinitions.h"],
    cmd = "m4 " +
          "-I $$(dirname $(location common/sys/elfdefinitions.m4)) " +
          "-D SRCDIR=$$(dirname $(location common/sys/elfdefinitions.m4))" +
          " $(location common/sys/elfdefinitions.m4) " +
          "> $@",
)

cc_library(
    name = "elf",
    srcs = glob([
        "common/*.h",
        "libelf/*.c",
        "libelf/*.h",
    ]) + [
        "libelf/libelf_convert.c",
        "libelf/libelf_fsize.c",
        "libelf/libelf_msize.c",
    ],
    hdrs = [
        "common/elfdefinitions.h",
        "common/sys/elfdefinitions.h",
        "libelf/gelf.h",
        "libelf/libelf.h",
    ],
    includes = [
        "common",
        "libelf",
    ],
    linkstatic = 1,
)

dwarf_nametbl_generated_files = [
    "libdwarf/dwarf_funcs",
    "libdwarf/dwarf_pubnames",
    "libdwarf/dwarf_pubtypes",
    "libdwarf/dwarf_types",
    "libdwarf/dwarf_vars",
    "libdwarf/dwarf_weaks",
]

dwarf_pro_nametbl_generated_files = [
    "libdwarf/dwarf_pro_funcs",
    "libdwarf/dwarf_pro_pubnames",
    "libdwarf/dwarf_pro_types",
    "libdwarf/dwarf_pro_vars",
    "libdwarf/dwarf_pro_weaks",
]

[genrule(
    name = "gen_%s" % generated_file,
    srcs = [
        "libdwarf/dwarf_nametbl.m4",
        "%s.m4" % generated_file,
    ],
    outs = ["%s.c" % generated_file],
    cmd = "m4 " +
          "-D SRCDIR=$$(dirname $(location %s.m4))" % generated_file +
          " $(location %s.m4) " % generated_file +
          "> $@",
) for generated_file in dwarf_nametbl_generated_files]

[genrule(
    name = "gen_%s" % generated_file,
    srcs = [
        "libdwarf/dwarf_pro_nametbl.m4",
        "%s.m4" % generated_file,
    ],
    outs = ["%s.c" % generated_file],
    cmd = "m4 " +
          "-D SRCDIR=$$(dirname $(location %s.m4))" % generated_file +
          " $(location %s.m4) " % generated_file +
          "> $@",
) for generated_file in dwarf_pro_nametbl_generated_files]


cc_library(
    name = "dwarf",
    srcs = glob([
        "common/*.h",
        "libdwarf/*.c",
        "libdwarf/*.h",
    ]) + [
        "libdwarf/dwarf_pubnames.c",
        "libdwarf/dwarf_pubtypes.c",
        "libdwarf/dwarf_weaks.c",
        "libdwarf/dwarf_funcs.c",
        "libdwarf/dwarf_vars.c",
        "libdwarf/dwarf_types.c",
        "libdwarf/dwarf_pro_pubnames.c",
        "libdwarf/dwarf_pro_weaks.c",
        "libdwarf/dwarf_pro_funcs.c",
        "libdwarf/dwarf_pro_types.c",
        "libdwarf/dwarf_pro_vars.c",
    ],
    hdrs = [
        "libdwarf/dwarf.h",
        "libdwarf/libdwarf.h",
    ],
    includes = [
        "common",
        "libdwarf",
    ],
    linkstatic = 1,
)
