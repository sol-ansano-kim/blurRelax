import sys
import excons
from excons.tools import maya


mayaver = excons.GetArgument("with-maya", None)
if mayaver is None:
    excons.SetArgument("with-maya", "2018")
    mayaver = "2018"


maya.SetupMscver()
env = excons.MakeBaseEnv()


customs = [maya.Require, maya.Plugin]

cppflags = ""
defs = []
prjs = []

if sys.platform != "win32":
    cppflags += " -Wno-unused-parameter"


prjs.append({"name": "xxhash",
             "alias": "xxhash",
             "type": "staticlib",
             "incdirs": ["external"],
             "srcs": ["external/xxhash.c"],
             "symvis": "default"})

prjs.append({"name": "blurRelax",
             "type": "dynamicmodule",
             "defs": defs,
             "cppflags": cppflags,
             "incdirs": ["external"],
             "ext": maya.PluginExt(),
             "prefix": mayaver,
             "libs": ["xxhash"],
             "libdirs": [excons.OutputBaseDirectory() + "/lib/"],
             "srcs": ["blurRelax.cpp"],
             "symvis": "default",
             "deps": ["xxhash"],
             "custom": customs})


targets = excons.DeclareTargets(env, prjs)
