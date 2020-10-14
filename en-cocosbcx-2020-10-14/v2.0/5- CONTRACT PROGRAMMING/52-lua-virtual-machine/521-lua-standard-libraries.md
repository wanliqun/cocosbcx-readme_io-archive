---
title: "5.2.1 Lua Standard Libraries"
slug: "521-lua-standard-libraries"
hidden: false
createdAt: "2019-06-25T03:14:23.435Z"
updatedAt: "2019-06-26T09:13:01.700Z"
---
The built-in virtual machine deletes certain contents of Lua standard libraries as follows:
[block:parameters]
{
  "data": {
    "h-0": "baselib",
    "0-0": "assert\ncollectgarbage\ndofile\nerror\ngetmetatable\nipairs\nload\nloadfile\nnext\npairs\npcall\nrawequal\nrawget\nrawlen\nrawset\nselect\nsetmetatable\ntonumber\ntostring\ntype\nxpcalldebug",
    "0-1": "concat\ninsert\nmove\npack\nremove\nsort\nunpack",
    "h-1": "tablelib",
    "h-2": "utf8lib",
    "0-2": "char\ncharpattern\ncodes\ncodepoint\nlen\noffset",
    "h-3": "stringlib",
    "h-4": "mathlib",
    "h-5": "coroutinelib",
    "0-3": "byte\nchar\ndump\nfind\nformat\ngmatch\ngsub\nlen\nlower\nmatch\npack\npacksize\nrep\nreverse\nsub\nunpack\nupper",
    "0-4": "abs\nacos\nasin\natan\natan2\nceil\ncos\ndeg\nexp\nfloor\nfrexp\nldexp\nlog\nlog10\nmax\nmin\nmod\nrad\nsin\nsqrt\ntan",
    "0-5": "create\nisyieldable\nresume\nrunning\nstatus\nwrap\nyield"
  },
  "cols": 6,
  "rows": 1
}
[/block]