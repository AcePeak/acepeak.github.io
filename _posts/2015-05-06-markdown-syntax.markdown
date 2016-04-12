---
layout: blogs_item
title: markdown语法支持的syntax高亮
author: AcePeak
categories:
  - 积累
tags:
  - Jekyll
  - Liquid
  - 转载
---

> http://pygments.org/docs/lexers/

{% highlight bash  %}

Lexers for ActionScript and MXML

class pygments.lexers.actionscript.ActionScript3Lexer
Short names:	as3, actionscript3
Filenames:	*.as
MIME types:	application/x-actionscript3, text/x-actionscript3, text/actionscript3
For ActionScript 3 source code.

New in version 0.11.

class pygments.lexers.actionscript.ActionScriptLexer
Short names:	as, actionscript
Filenames:	*.as
MIME types:	application/x-actionscript, text/x-actionscript, text/actionscript
For ActionScript source code.

New in version 0.9.

class pygments.lexers.actionscript.MxmlLexer
Short names:	mxml
Filenames:	*.mxml
MIME types:	None
For MXML markup. Nested AS3 in <script> tags is highlighted by the appropriate lexer.

New in version 1.1.

Lexers for computer algebra systems

class pygments.lexers.algebra.GAPLexer
Short names:	gap
Filenames:	*.g, *.gd, *.gi, *.gap
MIME types:	None
For GAP source code.

New in version 2.0.

class pygments.lexers.algebra.MathematicaLexer
Short names:	mathematica, mma, nb
Filenames:	*.nb, *.cdf, *.nbp, *.ma
MIME types:	application/mathematica, application/vnd.wolfram.mathematica, application/vnd.wolfram.mathematica.package, application/vnd.wolfram.cdf
Lexer for Mathematica source code.

New in version 2.0.

class pygments.lexers.algebra.MuPADLexer
Short names:	mupad
Filenames:	*.mu
MIME types:	None
A MuPAD lexer. Contributed by Christopher Creutzig <christopher@creutzig.de>.

New in version 0.8.

Lexers for AmbientTalk language

class pygments.lexers.ambient.AmbientTalkLexer
Short names:	at, ambienttalk, ambienttalk/2
Filenames:	*.at
MIME types:	text/x-ambienttalk
Lexer for AmbientTalk source code.

New in version 2.0.

Lexers for APL

class pygments.lexers.apl.APLLexer
Short names:	apl
Filenames:	*.apl
MIME types:	None
A simple APL lexer.

New in version 2.0.

Lexers for assembly languages

class pygments.lexers.asm.CObjdumpLexer
Short names:	c-objdump
Filenames:	*.c-objdump
MIME types:	text/x-c-objdump
For the output of ‘objdump -Sr on compiled C files’

class pygments.lexers.asm.Ca65Lexer
Short names:	ca65
Filenames:	*.s
MIME types:	None
For ca65 assembler sources.

New in version 1.6.

class pygments.lexers.asm.CppObjdumpLexer
Short names:	cpp-objdump, c++-objdumb, cxx-objdump
Filenames:	*.cpp-objdump, *.c++-objdump, *.cxx-objdump
MIME types:	text/x-cpp-objdump
For the output of ‘objdump -Sr on compiled C++ files’

class pygments.lexers.asm.DObjdumpLexer
Short names:	d-objdump
Filenames:	*.d-objdump
MIME types:	text/x-d-objdump
For the output of ‘objdump -Sr on compiled D files’

class pygments.lexers.asm.GasLexer
Short names:	gas, asm
Filenames:	*.s, *.S
MIME types:	text/x-gas
For Gas (AT&T) assembly code.

class pygments.lexers.asm.LlvmLexer
Short names:	llvm
Filenames:	*.ll
MIME types:	text/x-llvm
For LLVM assembly code.

class pygments.lexers.asm.NasmLexer
Short names:	nasm
Filenames:	*.asm, *.ASM
MIME types:	text/x-nasm
For Nasm (Intel) assembly code.

class pygments.lexers.asm.NasmObjdumpLexer
Short names:	objdump-nasm
Filenames:	*.objdump-intel
MIME types:	text/x-nasm-objdump
For the output of ‘objdump -d -M intel’.

New in version 2.0.

class pygments.lexers.asm.ObjdumpLexer
Short names:	objdump
Filenames:	*.objdump
MIME types:	text/x-objdump
For the output of ‘objdump -dr’

Lexers for automation scripting languages

class pygments.lexers.automation.AutoItLexer
Short names:	autoit
Filenames:	*.au3
MIME types:	text/x-autoit
For AutoIt files.

AutoIt is a freeware BASIC-like scripting language designed for automating the Windows GUI and general scripting

New in version 1.6.

class pygments.lexers.automation.AutohotkeyLexer
Short names:	ahk, autohotkey
Filenames:	*.ahk, *.ahkl
MIME types:	text/x-autohotkey
For autohotkey source code.

New in version 1.4.

Lexers for BASIC like languages (other than VB.net)

class pygments.lexers.basic.BlitzBasicLexer
Short names:	blitzbasic, b3d, bplus
Filenames:	*.bb, *.decls
MIME types:	text/x-bb
For BlitzBasic source code.

New in version 2.0.

class pygments.lexers.basic.BlitzMaxLexer
Short names:	blitzmax, bmax
Filenames:	*.bmx
MIME types:	text/x-bmx
For BlitzMax source code.

New in version 1.4.

class pygments.lexers.basic.CbmBasicV2Lexer
Short names:	cbmbas
Filenames:	*.bas
MIME types:	None
For CBM BASIC V2 sources.

New in version 1.6.

class pygments.lexers.basic.MonkeyLexer
Short names:	monkey
Filenames:	*.monkey
MIME types:	text/x-monkey
For Monkey source code.

New in version 1.6.

class pygments.lexers.basic.QBasicLexer
Short names:	qbasic, basic
Filenames:	*.BAS, *.bas
MIME types:	text/basic
For QBasic source code.

New in version 2.0.

Lexers for “business-oriented” languages

class pygments.lexers.business.ABAPLexer
Short names:	abap
Filenames:	*.abap
MIME types:	text/x-abap
Lexer for ABAP, SAP’s integrated language.

New in version 1.1.

class pygments.lexers.business.CobolFreeformatLexer
Short names:	cobolfree
Filenames:	*.cbl, *.CBL
MIME types:	None
Lexer for Free format OpenCOBOL code.

New in version 1.6.

class pygments.lexers.business.CobolLexer
Short names:	cobol
Filenames:	*.cob, *.COB, *.cpy, *.CPY
MIME types:	text/x-cobol
Lexer for OpenCOBOL code.

New in version 1.6.

class pygments.lexers.business.GoodDataCLLexer
Short names:	gooddata-cl
Filenames:	*.gdc
MIME types:	text/x-gooddata-cl
Lexer for GoodData-CL script files.

New in version 1.4.

class pygments.lexers.business.MaqlLexer
Short names:	maql
Filenames:	*.maql
MIME types:	text/x-gooddata-maql, application/x-gooddata-maql
Lexer for GoodData MAQL scripts.

New in version 1.4.

class pygments.lexers.business.OpenEdgeLexer
Short names:	openedge, abl, progress
Filenames:	*.p, *.cls
MIME types:	text/x-openedge, application/x-openedge
Lexer for OpenEdge ABL (formerly Progress) source code.

New in version 1.5.

Lexers for C/C++ languages

class pygments.lexers.c_cpp.CLexer
Short names:	c
Filenames:	*.c, *.h, *.idc
MIME types:	text/x-chdr, text/x-csrc
For C source code with preprocessor directives.

class pygments.lexers.c_cpp.CppLexer
Short names:	cpp, c++
Filenames:	*.cpp, *.hpp, *.c++, *.h++, *.cc, *.hh, *.cxx, *.hxx, *.C, *.H, *.cp, *.CPP
MIME types:	text/x-c++hdr, text/x-c++src
For C++ source code with preprocessor directives.

Lexers for other C-like languages

class pygments.lexers.c_like.ClayLexer
Short names:	clay
Filenames:	*.clay
MIME types:	text/x-clay
For Clay source.

New in version 2.0.

class pygments.lexers.c_like.CudaLexer
Short names:	cuda, cu
Filenames:	*.cu, *.cuh
MIME types:	text/x-cuda
For NVIDIA CUDA™ source.

New in version 1.6.

class pygments.lexers.c_like.ECLexer
Short names:	ec
Filenames:	*.ec, *.eh
MIME types:	text/x-echdr, text/x-ecsrc
For eC source code with preprocessor directives.

New in version 1.5.

class pygments.lexers.c_like.MqlLexer
Short names:	mql, mq4, mq5, mql4, mql5
Filenames:	*.mq4, *.mq5, *.mqh
MIME types:	text/x-mql
For MQL4 and MQL5 source code.

New in version 2.0.

class pygments.lexers.c_like.NesCLexer
Short names:	nesc
Filenames:	*.nc
MIME types:	text/x-nescsrc
For nesC source code with preprocessor directives.

New in version 2.0.

class pygments.lexers.c_like.PikeLexer
Short names:	pike
Filenames:	*.pike, *.pmod
MIME types:	text/x-pike
For Pike source code.

New in version 2.0.

class pygments.lexers.c_like.SwigLexer
Short names:	swig
Filenames:	*.swg, *.i
MIME types:	text/swig
For SWIG source code.

New in version 2.0.

class pygments.lexers.c_like.ValaLexer
Short names:	vala, vapi
Filenames:	*.vala, *.vapi
MIME types:	text/x-vala
For Vala source code with preprocessor directives.

New in version 1.1.

Lexer for the Chapel language

class pygments.lexers.chapel.ChapelLexer
Short names:	chapel, chpl
Filenames:	*.chpl
MIME types:	None
For Chapel source.

New in version 2.0.

Lexers for configuration file formats

class pygments.lexers.configs.ApacheConfLexer
Short names:	apacheconf, aconf, apache
Filenames:	.htaccess, apache.conf, apache2.conf
MIME types:	text/x-apacheconf
Lexer for configuration files following the Apache config file format.

New in version 0.6.

class pygments.lexers.configs.Cfengine3Lexer
Short names:	cfengine3, cf3
Filenames:	*.cf
MIME types:	None
Lexer for CFEngine3 policy files.

New in version 1.5.

class pygments.lexers.configs.DockerLexer
Short names:	docker, dockerfile
Filenames:	Dockerfile, *.docker
MIME types:	text/x-dockerfile-config
Lexer for Docker configuration files.

New in version 2.0.

class pygments.lexers.configs.IniLexer
Short names:	ini, cfg, dosini
Filenames:	*.ini, *.cfg
MIME types:	text/x-ini
Lexer for configuration files in INI style.

class pygments.lexers.configs.KconfigLexer
Short names:	kconfig, menuconfig, linux-config, kernel-config
Filenames:	Kconfig, *Config.in*, external.in*, standard-modules.in
MIME types:	text/x-kconfig
For Linux-style Kconfig files.

New in version 1.6.

class pygments.lexers.configs.LighttpdConfLexer
Short names:	lighty, lighttpd
Filenames:	None
MIME types:	text/x-lighttpd-conf
Lexer for Lighttpd configuration files.

New in version 0.11.

class pygments.lexers.configs.NginxConfLexer
Short names:	nginx
Filenames:	None
MIME types:	text/x-nginx-conf
Lexer for Nginx configuration files.

New in version 0.11.

class pygments.lexers.configs.PropertiesLexer
Short names:	properties, jproperties
Filenames:	*.properties
MIME types:	text/x-java-properties
Lexer for configuration files in Java’s properties format.

New in version 1.4.

class pygments.lexers.configs.RegeditLexer
Short names:	registry
Filenames:	*.reg
MIME types:	text/x-windows-registry
Lexer for Windows Registry files produced by regedit.

New in version 1.6.

class pygments.lexers.configs.SquidConfLexer
Short names:	squidconf, squid.conf, squid
Filenames:	squid.conf
MIME types:	text/x-squidconf
Lexer for squid configuration files.

New in version 0.9.

Lexers for misc console output

class pygments.lexers.console.PyPyLogLexer
Short names:	pypylog, pypy
Filenames:	*.pypylog
MIME types:	application/x-pypylog
Lexer for PyPy log files.

New in version 1.5.

class pygments.lexers.console.VCTreeStatusLexer
Short names:	vctreestatus
Filenames:	None
MIME types:	None
For colorizing output of version control status commands, like “hg status” or “svn status”.

New in version 2.0.

Lexers for CSS and related stylesheet formats

class pygments.lexers.css.CssLexer
Short names:	css
Filenames:	*.css
MIME types:	text/css
For CSS (Cascading Style Sheets).

class pygments.lexers.css.SassLexer
Short names:	sass
Filenames:	*.sass
MIME types:	text/x-sass
For Sass stylesheets.

New in version 1.3.

class pygments.lexers.css.ScssLexer
Short names:	scss
Filenames:	*.scss
MIME types:	text/x-scss
For SCSS stylesheets.

Lexers for D languages

class pygments.lexers.d.CrocLexer
Short names:	croc
Filenames:	*.croc
MIME types:	text/x-crocsrc
For Croc source.

class pygments.lexers.d.DLexer
Short names:	d
Filenames:	*.d, *.di
MIME types:	text/x-dsrc
For D source.

New in version 1.2.

class pygments.lexers.d.MiniDLexer
Short names:	minid
Filenames:	None
MIME types:	text/x-minidsrc
For MiniD source. MiniD is now known as Croc.

Pygments lexers for Dalvik VM-related languages

class pygments.lexers.dalvik.SmaliLexer
Short names:	smali
Filenames:	*.smali
MIME types:	text/smali
For Smali (Android/Dalvik) assembly code.

New in version 1.6.

Lexers for data file format

class pygments.lexers.data.JsonLdLexer
Short names:	jsonld, json-ld
Filenames:	*.jsonld
MIME types:	application/ld+json
For JSON-LD linked data.

New in version 2.0.

class pygments.lexers.data.JsonLexer
Short names:	json
Filenames:	*.json
MIME types:	application/json
For JSON data structures.

New in version 1.5.

class pygments.lexers.data.YamlLexer
Short names:	yaml
Filenames:	*.yaml, *.yml
MIME types:	text/x-yaml
Lexer for YAML, a human-friendly data serialization language.

New in version 0.11.

Lexers for diff/patch formats

class pygments.lexers.diff.DarcsPatchLexer
Short names:	dpatch
Filenames:	*.dpatch, *.darcspatch
MIME types:	None
DarcsPatchLexer is a lexer for the various versions of the darcs patch format. Examples of this format are derived by commands such as darcs annotate --patch and darcs send.

New in version 0.10.

class pygments.lexers.diff.DiffLexer
Short names:	diff, udiff
Filenames:	*.diff, *.patch
MIME types:	text/x-diff, text/x-patch
Lexer for unified or context-style diffs or patches.

Lexers for .net languages

class pygments.lexers.dotnet.BooLexer
Short names:	boo
Filenames:	*.boo
MIME types:	text/x-boo
For Boo source code.

class pygments.lexers.dotnet.CSharpAspxLexer
Short names:	aspx-cs
Filenames:	*.aspx, *.asax, *.ascx, *.ashx, *.asmx, *.axd
MIME types:	None
Lexer for highlighting C# within ASP.NET pages.

class pygments.lexers.dotnet.CSharpLexer
Short names:	csharp, c#
Filenames:	*.cs
MIME types:	text/x-csharp
For C# source code.

Additional options accepted:

unicodelevel
Determines which Unicode characters this lexer allows for identifiers. The possible values are:

none – only the ASCII letters and numbers are allowed. This is the fastest selection.
basic – all Unicode characters from the specification except category Lo are allowed.
full – all Unicode characters as specified in the C# specs are allowed. Note that this means a considerable slowdown since the Lo category has more than 40,000 characters in it!
The default value is basic.

New in version 0.8.

class pygments.lexers.dotnet.FSharpLexer
Short names:	fsharp
Filenames:	*.fs, *.fsi
MIME types:	text/x-fsharp
For the F# language (version 3.0).

AAAAACK Strings http://research.microsoft.com/en-us/um/cambridge/projects/fsharp/manual/spec.html#_Toc335818775

New in version 1.5.

class pygments.lexers.dotnet.NemerleLexer
Short names:	nemerle
Filenames:	*.n
MIME types:	text/x-nemerle
For Nemerle source code.

Additional options accepted:

unicodelevel
Determines which Unicode characters this lexer allows for identifiers. The possible values are:

none – only the ASCII letters and numbers are allowed. This is the fastest selection.
basic – all Unicode characters from the specification except category Lo are allowed.
full – all Unicode characters as specified in the C# specs are allowed. Note that this means a considerable slowdown since the Lo category has more than 40,000 characters in it!
The default value is basic.

New in version 1.5.

class pygments.lexers.dotnet.VbNetAspxLexer
Short names:	aspx-vb
Filenames:	*.aspx, *.asax, *.ascx, *.ashx, *.asmx, *.axd
MIME types:	None
Lexer for highlighting Visual Basic.net within ASP.NET pages.

class pygments.lexers.dotnet.VbNetLexer
Short names:	vb.net, vbnet
Filenames:	*.vb, *.bas
MIME types:	text/x-vbnet, text/x-vba
For Visual Basic.NET source code.

Lexers for various domain-specific languages

class pygments.lexers.dsls.AlloyLexer
Short names:	alloy
Filenames:	*.als
MIME types:	text/x-alloy
For Alloy source code.

New in version 2.0.

class pygments.lexers.dsls.BroLexer
Short names:	bro
Filenames:	*.bro
MIME types:	None
For Bro scripts.

New in version 1.5.

class pygments.lexers.dsls.MscgenLexer
Short names:	mscgen, msc
Filenames:	*.msc
MIME types:	None
For Mscgen files.

New in version 1.6.

class pygments.lexers.dsls.PanLexer
Short names:	pan
Filenames:	*.pan
MIME types:	None
Lexer for pan source files.

Based on tcsh lexer.

New in version 2.0.

class pygments.lexers.dsls.ProtoBufLexer
Short names:	protobuf, proto
Filenames:	*.proto
MIME types:	None
Lexer for Protocol Buffer definition files.

New in version 1.4.

class pygments.lexers.dsls.PuppetLexer
Short names:	puppet
Filenames:	*.pp
MIME types:	None
For Puppet configuration DSL.

New in version 1.6.

class pygments.lexers.dsls.RslLexer
Short names:	rsl
Filenames:	*.rsl
MIME types:	text/rsl
RSL is the formal specification language used in RAISE (Rigorous Approach to Industrial Software Engineering) method.

New in version 2.0.

class pygments.lexers.dsls.VGLLexer
Short names:	vgl
Filenames:	*.rpf
MIME types:	None
For SampleManager VGL source code.

New in version 1.6.

Lexers for the Dylan language

class pygments.lexers.dylan.DylanConsoleLexer
Short names:	dylan-console, dylan-repl
Filenames:	*.dylan-console
MIME types:	text/x-dylan-console
For Dylan interactive console output like:

? let a = 1;
=> 1
? a
=> 1
This is based on a copy of the RubyConsoleLexer.

New in version 1.6.

class pygments.lexers.dylan.DylanLexer
Short names:	dylan
Filenames:	*.dylan, *.dyl, *.intr
MIME types:	text/x-dylan
For the Dylan language.

New in version 0.7.

class pygments.lexers.dylan.DylanLidLexer
Short names:	dylan-lid, lid
Filenames:	*.lid, *.hdp
MIME types:	text/x-dylan-lid
For Dylan LID (Library Interchange Definition) files.

New in version 1.6.

Lexers for the ECL language

class pygments.lexers.ecl.ECLLexer
Short names:	ecl
Filenames:	*.ecl
MIME types:	application/x-ecl
Lexer for the declarative big-data ECL language.

New in version 1.5.

Lexer for the Eiffel language

class pygments.lexers.eiffel.EiffelLexer
Short names:	eiffel
Filenames:	*.e
MIME types:	text/x-eiffel
For Eiffel source code.

New in version 2.0.

Lexers for Erlang

class pygments.lexers.erlang.ElixirConsoleLexer
Short names:	iex
Filenames:	None
MIME types:	text/x-elixir-shellsession
For Elixir interactive console (iex) output like:

iex> [head | tail] = [1,2,3]
[1,2,3]
iex> head
1
iex> tail
[2,3]
iex> [head | tail]
[1,2,3]
iex> length [head | tail]
3
New in version 1.5.

class pygments.lexers.erlang.ElixirLexer
Short names:	elixir, ex, exs
Filenames:	*.ex, *.exs
MIME types:	text/x-elixir
For the Elixir language.

New in version 1.5.

class pygments.lexers.erlang.ErlangLexer
Short names:	erlang
Filenames:	*.erl, *.hrl, *.es, *.escript
MIME types:	text/x-erlang
For the Erlang functional programming language.

Blame Jeremy Thurgood (http://jerith.za.net/).

New in version 0.9.

class pygments.lexers.erlang.ErlangShellLexer
Short names:	erl
Filenames:	*.erl-sh
MIME types:	text/x-erl-shellsession
Shell sessions in erl (for Erlang code).

New in version 1.1.

Lexers for esoteric languages

class pygments.lexers.esoteric.BefungeLexer
Short names:	befunge
Filenames:	*.befunge
MIME types:	application/x-befunge
Lexer for the esoteric Befunge language.

New in version 0.7.

class pygments.lexers.esoteric.BrainfuckLexer
Short names:	brainfuck, bf
Filenames:	*.bf, *.b
MIME types:	application/x-brainfuck
Lexer for the esoteric BrainFuck language.

class pygments.lexers.esoteric.RedcodeLexer
Short names:	redcode
Filenames:	*.cw
MIME types:	None
A simple Redcode lexer based on ICWS‘94. Contributed by Adam Blinkinsop <blinks@acm.org>.

New in version 0.8.

Lexers for the Factor language

class pygments.lexers.factor.FactorLexer
Short names:	factor
Filenames:	*.factor
MIME types:	text/x-factor
Lexer for the Factor language.

New in version 1.4.

Lexer for the Fantom language

class pygments.lexers.fantom.FantomLexer
Short names:	fan
Filenames:	*.fan
MIME types:	application/x-fantom
For Fantom source code.

New in version 1.5.

Lexer for the Felix language

class pygments.lexers.felix.FelixLexer
Short names:	felix, flx
Filenames:	*.flx, *.flxh
MIME types:	text/x-felix
For Felix source code.

New in version 1.2.

Lexers for Fortran languages

class pygments.lexers.fortran.FortranLexer
Short names:	fortran
Filenames:	*.f, *.f90, *.F, *.F90
MIME types:	text/x-fortran
Lexer for FORTRAN 90 code.

New in version 0.10.

Simple lexer for Microsoft Visual FoxPro source code

class pygments.lexers.foxpro.FoxProLexer
Short names:	foxpro, vfp, clipper, xbase
Filenames:	*.PRG, *.prg
MIME types:	None
Lexer for Microsoft Visual FoxPro language.

FoxPro syntax allows to shorten all keywords and function names to 4 characters. Shortened forms are not recognized by this lexer.

New in version 1.6.

Lexers for the Google Go language

class pygments.lexers.go.GoLexer
Short names:	go
Filenames:	*.go
MIME types:	text/x-gosrc
For Go source.

New in version 1.2.

Lexers for graph query languages

class pygments.lexers.graph.CypherLexer
Short names:	cypher
Filenames:	*.cyp, *.cypher
MIME types:	None
For Cypher Query Language

For the Cypher version in Neo4J 2.0

New in version 2.0.

Lexers for computer graphics and plotting related languages

class pygments.lexers.graphics.AsymptoteLexer
Short names:	asy, asymptote
Filenames:	*.asy
MIME types:	text/x-asymptote
For Asymptote source code.

New in version 1.2.

class pygments.lexers.graphics.GLShaderLexer
Short names:	glsl
Filenames:	*.vert, *.frag, *.geo
MIME types:	text/x-glslsrc
GLSL (OpenGL Shader) lexer.

New in version 1.1.

class pygments.lexers.graphics.GnuplotLexer
Short names:	gnuplot
Filenames:	*.plot, *.plt
MIME types:	text/x-gnuplot
For Gnuplot plotting scripts.

New in version 0.11.

class pygments.lexers.graphics.PostScriptLexer
Short names:	postscript, postscr
Filenames:	*.ps, *.eps
MIME types:	application/postscript
Lexer for PostScript files.

The PostScript Language Reference published by Adobe at <http://partners.adobe.com/public/developer/en/ps/PLRM.pdf> is the authority for this.

New in version 1.4.

class pygments.lexers.graphics.PovrayLexer
Short names:	pov
Filenames:	*.pov, *.inc
MIME types:	text/x-povray
For Persistence of Vision Raytracer files.

New in version 0.11.

Lexers for Haskell and related languages

class pygments.lexers.haskell.AgdaLexer
Short names:	agda
Filenames:	*.agda
MIME types:	text/x-agda
For the Agda dependently typed functional programming language and proof assistant.

New in version 2.0.

class pygments.lexers.haskell.CryptolLexer
Short names:	cryptol, cry
Filenames:	*.cry
MIME types:	text/x-cryptol
FIXME: A Cryptol2 lexer based on the lexemes defined in the Haskell 98 Report.

New in version 2.0.

class pygments.lexers.haskell.HaskellLexer
Short names:	haskell, hs
Filenames:	*.hs
MIME types:	text/x-haskell
A Haskell lexer based on the lexemes defined in the Haskell 98 Report.

New in version 0.8.

class pygments.lexers.haskell.IdrisLexer
Short names:	idris, idr
Filenames:	*.idr
MIME types:	text/x-idris
A lexer for the dependently typed programming language Idris.

Based on the Haskell and Agda Lexer.

New in version 2.0.

class pygments.lexers.haskell.KokaLexer
Short names:	koka
Filenames:	*.kk, *.kki
MIME types:	text/x-koka
Lexer for the Koka language.

New in version 1.6.

class pygments.lexers.haskell.LiterateAgdaLexer
Short names:	lagda, literate-agda
Filenames:	*.lagda
MIME types:	text/x-literate-agda
For Literate Agda source.

Additional options accepted:

litstyle
If given, must be "bird" or "latex". If not given, the style is autodetected: if the first non-whitespace character in the source is a backslash or percent character, LaTeX is assumed, else Bird.
New in version 2.0.

class pygments.lexers.haskell.LiterateCryptolLexer
Short names:	lcry, literate-cryptol, lcryptol
Filenames:	*.lcry
MIME types:	text/x-literate-cryptol
For Literate Cryptol (Bird-style or LaTeX) source.

Additional options accepted:

litstyle
If given, must be "bird" or "latex". If not given, the style is autodetected: if the first non-whitespace character in the source is a backslash or percent character, LaTeX is assumed, else Bird.
New in version 2.0.

class pygments.lexers.haskell.LiterateHaskellLexer
Short names:	lhs, literate-haskell, lhaskell
Filenames:	*.lhs
MIME types:	text/x-literate-haskell
For Literate Haskell (Bird-style or LaTeX) source.

Additional options accepted:

litstyle
If given, must be "bird" or "latex". If not given, the style is autodetected: if the first non-whitespace character in the source is a backslash or percent character, LaTeX is assumed, else Bird.
New in version 0.9.

class pygments.lexers.haskell.LiterateIdrisLexer
Short names:	lidr, literate-idris, lidris
Filenames:	*.lidr
MIME types:	text/x-literate-idris
For Literate Idris (Bird-style or LaTeX) source.

Additional options accepted:

litstyle
If given, must be "bird" or "latex". If not given, the style is autodetected: if the first non-whitespace character in the source is a backslash or percent character, LaTeX is assumed, else Bird.
New in version 2.0.

Lexers for Haxe and related stuff

class pygments.lexers.haxe.HaxeLexer
Short names:	hx, haxe, hxsl
Filenames:	*.hx, *.hxsl
MIME types:	text/haxe, text/x-haxe, text/x-hx
For Haxe source code (http://haxe.org/).

New in version 1.3.

class pygments.lexers.haxe.HxmlLexer
Short names:	haxeml, hxml
Filenames:	*.hxml
MIME types:	None
Lexer for haXe build files.

New in version 1.6.

Lexers for hardware descriptor languages

class pygments.lexers.hdl.SystemVerilogLexer
Short names:	systemverilog, sv
Filenames:	*.sv, *.svh
MIME types:	text/x-systemverilog
Extends verilog lexer to recognise all SystemVerilog keywords from IEEE 1800-2009 standard.

New in version 1.5.

class pygments.lexers.hdl.VerilogLexer
Short names:	verilog, v
Filenames:	*.v
MIME types:	text/x-verilog
For verilog source code with preprocessor directives.

New in version 1.4.

class pygments.lexers.hdl.VhdlLexer
Short names:	vhdl
Filenames:	*.vhdl, *.vhd
MIME types:	text/x-vhdl
For VHDL source code.

New in version 1.5.

Lexers for HTML, XML and related markup

class pygments.lexers.html.DtdLexer
Short names:	dtd
Filenames:	*.dtd
MIME types:	application/xml-dtd
A lexer for DTDs (Document Type Definitions).

New in version 1.5.

class pygments.lexers.html.HamlLexer
Short names:	haml
Filenames:	*.haml
MIME types:	text/x-haml
For Haml markup.

New in version 1.3.

class pygments.lexers.html.HtmlLexer
Short names:	html
Filenames:	*.html, *.htm, *.xhtml, *.xslt
MIME types:	text/html, application/xhtml+xml
For HTML 4 and XHTML 1 markup. Nested JavaScript and CSS is highlighted by the appropriate lexer.

class pygments.lexers.html.JadeLexer
Short names:	jade
Filenames:	*.jade
MIME types:	text/x-jade
For Jade markup. Jade is a variant of Scaml, see: http://scalate.fusesource.org/documentation/scaml-reference.html

New in version 1.4.

class pygments.lexers.html.ScamlLexer
Short names:	scaml
Filenames:	*.scaml
MIME types:	text/x-scaml
For Scaml markup. Scaml is Haml for Scala.

New in version 1.4.

class pygments.lexers.html.XmlLexer
Short names:	xml
Filenames:	*.xml, *.xsl, *.rss, *.xslt, *.xsd, *.wsdl, *.wsf
MIME types:	text/xml, application/xml, image/svg+xml, application/rss+xml, application/atom+xml
Generic lexer for XML (eXtensible Markup Language).

class pygments.lexers.html.XsltLexer
Short names:	xslt
Filenames:	*.xsl, *.xslt, *.xpl
MIME types:	application/xsl+xml, application/xslt+xml
A lexer for XSLT.

New in version 0.10.

Lexers for IDL

class pygments.lexers.idl.IDLLexer
Short names:	idl
Filenames:	*.pro
MIME types:	text/idl
Pygments Lexer for IDL (Interactive Data Language).

New in version 1.6.

Lexers for Igor Pro

class pygments.lexers.igor.IgorLexer
Short names:	igor, igorpro
Filenames:	*.ipf
MIME types:	text/ipf
Pygments Lexer for Igor Pro procedure files (.ipf). See http://www.wavemetrics.com/ and http://www.igorexchange.com/.

New in version 2.0.

Lexers for Inferno os and all the related stuff

class pygments.lexers.inferno.LimboLexer
Short names:	limbo
Filenames:	*.b
MIME types:	text/limbo
Lexer for Limbo programming language

TODO:
maybe implement better var declaration highlighting
some simple syntax error highlighting
New in version 2.0.

Lexers for installer/packager DSLs and formats

class pygments.lexers.installers.DebianControlLexer
Short names:	control, debcontrol
Filenames:	control
MIME types:	None
Lexer for Debian control files and apt-cache show <pkg> outputs.

New in version 0.9.

class pygments.lexers.installers.NSISLexer
Short names:	nsis, nsi, nsh
Filenames:	*.nsi, *.nsh
MIME types:	text/x-nsis
For NSIS scripts.

New in version 1.6.

class pygments.lexers.installers.RPMSpecLexer
Short names:	spec
Filenames:	*.spec
MIME types:	text/x-rpm-spec
For RPM .spec files.

New in version 1.6.

class pygments.lexers.installers.SourcesListLexer
Short names:	sourceslist, sources.list, debsources
Filenames:	sources.list
MIME types:	None
Lexer that highlights debian sources.list files.

New in version 0.7.

Lexers for interactive fiction languages

class pygments.lexers.int_fiction.Inform6Lexer
Short names:	inform6, i6
Filenames:	*.inf
MIME types:	None
For Inform 6 source code.

New in version 2.0.

class pygments.lexers.int_fiction.Inform6TemplateLexer
Short names:	i6t
Filenames:	*.i6t
MIME types:	None
For Inform 6 template code.

New in version 2.0.

class pygments.lexers.int_fiction.Inform7Lexer
Short names:	inform7, i7
Filenames:	*.ni, *.i7x
MIME types:	None
For Inform 7 source code.

New in version 2.0.

class pygments.lexers.int_fiction.Tads3Lexer
Short names:	tads3
Filenames:	*.t
MIME types:	None
For TADS 3 source code.

Lexers for the Io language

class pygments.lexers.iolang.IoLexer
Short names:	io
Filenames:	*.io
MIME types:	text/x-iosrc
For Io (a small, prototype-based programming language) source.

New in version 0.10.

Lexers for JavaScript and related languages

class pygments.lexers.javascript.CoffeeScriptLexer
Short names:	coffee-script, coffeescript, coffee
Filenames:	*.coffee
MIME types:	text/coffeescript
For CoffeeScript source code.

New in version 1.3.

class pygments.lexers.javascript.DartLexer
Short names:	dart
Filenames:	*.dart
MIME types:	text/x-dart
For Dart source code.

New in version 1.5.

class pygments.lexers.javascript.JavascriptLexer
Short names:	js, javascript
Filenames:	*.js
MIME types:	application/javascript, application/x-javascript, text/x-javascript, text/javascript
For JavaScript source code.

class pygments.lexers.javascript.KalLexer
Short names:	kal
Filenames:	*.kal
MIME types:	text/kal, application/kal
For Kal source code.

New in version 2.0.

class pygments.lexers.javascript.LassoLexer
Short names:	lasso, lassoscript
Filenames:	*.lasso, *.lasso[89]
MIME types:	text/x-lasso
For Lasso source code, covering both Lasso 9 syntax and LassoScript for Lasso 8.6 and earlier. For Lasso embedded in HTML, use the LassoHtmlLexer.

Additional options accepted:

builtinshighlighting
If given and True, highlight builtin types, traits, methods, and members (default: True).
requiredelimiters
If given and True, only highlight code between delimiters as Lasso (default: False).
New in version 1.6.

class pygments.lexers.javascript.LiveScriptLexer
Short names:	live-script, livescript
Filenames:	*.ls
MIME types:	text/livescript
For LiveScript source code.

New in version 1.6.

class pygments.lexers.javascript.MaskLexer
Short names:	mask
Filenames:	*.mask
MIME types:	text/x-mask
For Mask markup.

New in version 2.0.

class pygments.lexers.javascript.ObjectiveJLexer
Short names:	objective-j, objectivej, obj-j, objj
Filenames:	*.j
MIME types:	text/x-objective-j
For Objective-J source code with preprocessor directives.

New in version 1.3.

class pygments.lexers.javascript.TypeScriptLexer
Short names:	ts
Filenames:	*.ts
MIME types:	text/x-typescript
For TypeScript source code.

New in version 1.6.

Lexers for the Julia language

class pygments.lexers.julia.JuliaConsoleLexer
Short names:	jlcon
Filenames:	None
MIME types:	None
For Julia console sessions. Modeled after MatlabSessionLexer.

New in version 1.6.

class pygments.lexers.julia.JuliaLexer
Short names:	julia, jl
Filenames:	*.jl
MIME types:	text/x-julia, application/x-julia
For Julia source code.

New in version 1.6.

Pygments lexers for JVM languages

class pygments.lexers.jvm.AspectJLexer
Short names:	aspectj
Filenames:	*.aj
MIME types:	text/x-aspectj
For AspectJ source code.

New in version 1.6.

class pygments.lexers.jvm.CeylonLexer
Short names:	ceylon
Filenames:	*.ceylon
MIME types:	text/x-ceylon
For Ceylon source code.

New in version 1.6.

class pygments.lexers.jvm.ClojureLexer
Short names:	clojure, clj
Filenames:	*.clj
MIME types:	text/x-clojure, application/x-clojure
Lexer for Clojure source code.

New in version 0.11.

class pygments.lexers.jvm.ClojureScriptLexer
Short names:	clojurescript, cljs
Filenames:	*.cljs
MIME types:	text/x-clojurescript, application/x-clojurescript
Lexer for ClojureScript source code.

New in version 2.0.

class pygments.lexers.jvm.GoloLexer
Short names:	golo
Filenames:	*.golo
MIME types:	None
For Golo source code.

New in version 2.0.

class pygments.lexers.jvm.GosuLexer
Short names:	gosu
Filenames:	*.gs, *.gsx, *.gsp, *.vark
MIME types:	text/x-gosu
For Gosu source code.

New in version 1.5.

class pygments.lexers.jvm.GosuTemplateLexer
Short names:	gst
Filenames:	*.gst
MIME types:	text/x-gosu-template
For Gosu templates.

New in version 1.5.

class pygments.lexers.jvm.GroovyLexer
Short names:	groovy
Filenames:	*.groovy
MIME types:	text/x-groovy
For Groovy source code.

New in version 1.5.

class pygments.lexers.jvm.IokeLexer
Short names:	ioke, ik
Filenames:	*.ik
MIME types:	text/x-iokesrc
For Ioke (a strongly typed, dynamic, prototype based programming language) source.

New in version 1.4.

class pygments.lexers.jvm.JasminLexer
Short names:	jasmin, jasminxt
Filenames:	*.j
MIME types:	None
For Jasmin assembly code.

New in version 2.0.

class pygments.lexers.jvm.JavaLexer
Short names:	java
Filenames:	*.java
MIME types:	text/x-java
For Java source code.

class pygments.lexers.jvm.KotlinLexer
Short names:	kotlin
Filenames:	*.kt
MIME types:	text/x-kotlin
For Kotlin source code.

New in version 1.5.

class pygments.lexers.jvm.PigLexer
Short names:	pig
Filenames:	*.pig
MIME types:	text/x-pig
For Pig Latin source code.

New in version 2.0.

class pygments.lexers.jvm.ScalaLexer
Short names:	scala
Filenames:	*.scala
MIME types:	text/x-scala
For Scala source code.

class pygments.lexers.jvm.XtendLexer
Short names:	xtend
Filenames:	*.xtend
MIME types:	text/x-xtend
For Xtend source code.

New in version 1.6.

Lexers for Lispy languages

class pygments.lexers.lisp.CommonLispLexer
Short names:	common-lisp, cl, lisp, elisp, emacs, emacs-lisp
Filenames:	*.cl, *.lisp, *.el
MIME types:	text/x-common-lisp
A Common Lisp lexer.

New in version 0.9.

class pygments.lexers.lisp.HyLexer
Short names:	hylang
Filenames:	*.hy
MIME types:	text/x-hy, application/x-hy
Lexer for Hy source code.

New in version 2.0.

class pygments.lexers.lisp.NewLispLexer
Short names:	newlisp
Filenames:	*.lsp, *.nl
MIME types:	text/x-newlisp, application/x-newlisp
For newLISP. source code (version 10.3.0).

New in version 1.5.

class pygments.lexers.lisp.RacketLexer
Short names:	racket, rkt
Filenames:	*.rkt, *.rktd, *.rktl
MIME types:	text/x-racket, application/x-racket
Lexer for Racket source code (formerly known as PLT Scheme).

New in version 1.6.

class pygments.lexers.lisp.SchemeLexer
Short names:	scheme, scm
Filenames:	*.scm, *.ss
MIME types:	text/x-scheme, application/x-scheme
A Scheme lexer, parsing a stream and outputting the tokens needed to highlight scheme code. This lexer could be most probably easily subclassed to parse other LISP-Dialects like Common Lisp, Emacs Lisp or AutoLisp.

This parser is checked with pastes from the LISP pastebin at http://paste.lisp.org/ to cover as much syntax as possible.

It supports the full Scheme syntax as defined in R5RS.

New in version 0.6.

Lexers for Makefiles and similar

class pygments.lexers.make.BaseMakefileLexer
Short names:	basemake
Filenames:	None
MIME types:	None
Lexer for simple Makefiles (no preprocessing).

New in version 0.10.

class pygments.lexers.make.CMakeLexer
Short names:	cmake
Filenames:	*.cmake, CMakeLists.txt
MIME types:	text/x-cmake
Lexer for CMake files.

New in version 1.2.

class pygments.lexers.make.MakefileLexer
Short names:	make, makefile, mf, bsdmake
Filenames:	*.mak, *.mk, Makefile, makefile, Makefile.*, GNUmakefile
MIME types:	text/x-makefile
Lexer for BSD and GNU make extensions (lenient enough to handle both in the same file even).

Rewritten in Pygments 0.10.

Lexers for non-HTML markup languages

class pygments.lexers.markup.BBCodeLexer
Short names:	bbcode
Filenames:	None
MIME types:	text/x-bbcode
A lexer that highlights BBCode(-like) syntax.

New in version 0.6.

class pygments.lexers.markup.GroffLexer
Short names:	groff, nroff, man
Filenames:	*.[1234567], *.man
MIME types:	application/x-troff, text/troff
Lexer for the (g)roff typesetting language, supporting groff extensions. Mainly useful for highlighting manpage sources.

New in version 0.6.

class pygments.lexers.markup.MoinWikiLexer
Short names:	trac-wiki, moin
Filenames:	None
MIME types:	text/x-trac-wiki
For MoinMoin (and Trac) Wiki markup.

New in version 0.7.

class pygments.lexers.markup.MozPreprocCssLexer
Short names:	css+mozpreproc
Filenames:	*.css.in
MIME types:	None
Subclass of the MozPreprocHashLexer that highlights unlexed data with the CssLexer.

New in version 2.0.

class pygments.lexers.markup.MozPreprocHashLexer
Short names:	mozhashpreproc
Filenames:	None
MIME types:	None
Lexer for Mozilla Preprocessor files (with ‘#’ as the marker).

Other data is left untouched.

New in version 2.0.

class pygments.lexers.markup.MozPreprocJavascriptLexer
Short names:	javascript+mozpreproc
Filenames:	*.js.in
MIME types:	None
Subclass of the MozPreprocHashLexer that highlights unlexed data with the JavascriptLexer.

New in version 2.0.

class pygments.lexers.markup.MozPreprocPercentLexer
Short names:	mozpercentpreproc
Filenames:	None
MIME types:	None
Lexer for Mozilla Preprocessor files (with ‘%’ as the marker).

Other data is left untouched.

New in version 2.0.

class pygments.lexers.markup.MozPreprocXulLexer
Short names:	xul+mozpreproc
Filenames:	*.xul.in
MIME types:	None
Subclass of the MozPreprocHashLexer that highlights unlexed data with the XmlLexer.

New in version 2.0.

class pygments.lexers.markup.RstLexer
Short names:	rst, rest, restructuredtext
Filenames:	*.rst, *.rest
MIME types:	text/x-rst, text/prs.fallenstein.rst
For reStructuredText markup.

New in version 0.7.

Additional options accepted:

handlecodeblocks
Highlight the contents of .. sourcecode:: language, .. code:: language and .. code-block:: language directives with a lexer for the given language (default: True).

New in version 0.8.

class pygments.lexers.markup.TexLexer
Short names:	tex, latex
Filenames:	*.tex, *.aux, *.toc
MIME types:	text/x-tex, text/x-latex
Lexer for the TeX and LaTeX typesetting languages.

Lexers for Matlab and related languages

class pygments.lexers.matlab.MatlabLexer
Short names:	matlab
Filenames:	*.m
MIME types:	text/matlab
For Matlab source code.

New in version 0.10.

class pygments.lexers.matlab.MatlabSessionLexer
Short names:	matlabsession
Filenames:	None
MIME types:	None
For Matlab sessions. Modeled after PythonConsoleLexer. Contributed by Ken Schutte <kschutte@csail.mit.edu>.

New in version 0.10.

class pygments.lexers.matlab.OctaveLexer
Short names:	octave
Filenames:	*.m
MIME types:	text/octave
For GNU Octave source code.

New in version 1.5.

class pygments.lexers.matlab.ScilabLexer
Short names:	scilab
Filenames:	*.sci, *.sce, *.tst
MIME types:	text/scilab
For Scilab source code.

New in version 1.5.

Lexers for ML family languages

class pygments.lexers.ml.OcamlLexer
Short names:	ocaml
Filenames:	*.ml, *.mli, *.mll, *.mly
MIME types:	text/x-ocaml
For the OCaml language.

New in version 0.7.

class pygments.lexers.ml.OpaLexer
Short names:	opa
Filenames:	*.opa
MIME types:	text/x-opa
Lexer for the Opa language (http://opalang.org).

New in version 1.5.

class pygments.lexers.ml.SMLLexer
Short names:	sml
Filenames:	*.sml, *.sig, *.fun
MIME types:	text/x-standardml, application/x-standardml
For the Standard ML language.

New in version 1.5.

Lexers for modeling languages

class pygments.lexers.modeling.BugsLexer
Short names:	bugs, winbugs, openbugs
Filenames:	*.bug
MIME types:	None
Pygments Lexer for OpenBugs and WinBugs models.

New in version 1.6.

class pygments.lexers.modeling.JagsLexer
Short names:	jags
Filenames:	*.jag, *.bug
MIME types:	None
Pygments Lexer for JAGS.

New in version 1.6.

class pygments.lexers.modeling.ModelicaLexer
Short names:	modelica
Filenames:	*.mo
MIME types:	text/x-modelica
For Modelica source code.

New in version 1.1.

class pygments.lexers.modeling.StanLexer
Short names:	stan
Filenames:	*.stan
MIME types:	None
Pygments Lexer for Stan models.

The Stan modeling language is specified in the Stan Modeling Language User’s Guide and Reference Manual, v2.4.0, pdf.

New in version 1.6.

Lexer for the Nimrod language

class pygments.lexers.nimrod.NimrodLexer
Short names:	nimrod, nim
Filenames:	*.nim, *.nimrod
MIME types:	text/x-nimrod
For Nimrod source code.

New in version 1.5.

Lexer for the Nit language

class pygments.lexers.nit.NitLexer
Short names:	nit
Filenames:	*.nit
MIME types:	None
For nit source.

New in version 2.0.

Lexers for the NixOS Nix language

class pygments.lexers.nix.NixLexer
Short names:	nixos, nix
Filenames:	*.nix
MIME types:	text/x-nix
For the Nix language.

New in version 2.0.

Lexers for Objective-C family languages

class pygments.lexers.objective.LogosLexer
Short names:	logos
Filenames:	*.x, *.xi, *.xm, *.xmi
MIME types:	text/x-logos
For Logos + Objective-C source code with preprocessor directives.

New in version 1.6.

class pygments.lexers.objective.ObjectiveCLexer
Short names:	objective-c, objectivec, obj-c, objc
Filenames:	*.m, *.h
MIME types:	text/x-objective-c
For Objective-C source code with preprocessor directives.

class pygments.lexers.objective.ObjectiveCppLexer
Short names:	objective-c++, objectivec++, obj-c++, objc++
Filenames:	*.mm, *.hh
MIME types:	text/x-objective-c++
For Objective-C++ source code with preprocessor directives.

class pygments.lexers.objective.SwiftLexer
Short names:	swift
Filenames:	*.swift
MIME types:	text/x-swift
For Swift source.

New in version 2.0.

Lexers for the Ooc language

class pygments.lexers.ooc.OocLexer
Short names:	ooc
Filenames:	*.ooc
MIME types:	text/x-ooc
For Ooc source code

New in version 1.2.

Lexers for parser generators

class pygments.lexers.parsers.AntlrActionScriptLexer
Short names:	antlr-as, antlr-actionscript
Filenames:	*.G, *.g
MIME types:	None
ANTLR with ActionScript Target

New in version 1.1.

class pygments.lexers.parsers.AntlrCSharpLexer
Short names:	antlr-csharp, antlr-c#
Filenames:	*.G, *.g
MIME types:	None
ANTLR with C# Target

New in version 1.1.

class pygments.lexers.parsers.AntlrCppLexer
Short names:	antlr-cpp
Filenames:	*.G, *.g
MIME types:	None
ANTLR with CPP Target

New in version 1.1.

class pygments.lexers.parsers.AntlrJavaLexer
Short names:	antlr-java
Filenames:	*.G, *.g
MIME types:	None
ANTLR with Java Target

New in version 1..

class pygments.lexers.parsers.AntlrLexer
Short names:	antlr
Filenames:	None
MIME types:	None
Generic ANTLR Lexer. Should not be called directly, instead use DelegatingLexer for your target language.

New in version 1.1.

class pygments.lexers.parsers.AntlrObjectiveCLexer
Short names:	antlr-objc
Filenames:	*.G, *.g
MIME types:	None
ANTLR with Objective-C Target

New in version 1.1.

class pygments.lexers.parsers.AntlrPerlLexer
Short names:	antlr-perl
Filenames:	*.G, *.g
MIME types:	None
ANTLR with Perl Target

New in version 1.1.

class pygments.lexers.parsers.AntlrPythonLexer
Short names:	antlr-python
Filenames:	*.G, *.g
MIME types:	None
ANTLR with Python Target

New in version 1.1.

class pygments.lexers.parsers.AntlrRubyLexer
Short names:	antlr-ruby, antlr-rb
Filenames:	*.G, *.g
MIME types:	None
ANTLR with Ruby Target

New in version 1.1.

class pygments.lexers.parsers.EbnfLexer
Short names:	ebnf
Filenames:	*.ebnf
MIME types:	text/x-ebnf
Lexer for ISO/IEC 14977 EBNF grammars.

New in version 2.0.

class pygments.lexers.parsers.RagelCLexer
Short names:	ragel-c
Filenames:	*.rl
MIME types:	None
A lexer for Ragel in a C host file.

New in version 1.1.

class pygments.lexers.parsers.RagelCppLexer
Short names:	ragel-cpp
Filenames:	*.rl
MIME types:	None
A lexer for Ragel in a CPP host file.

New in version 1.1.

class pygments.lexers.parsers.RagelDLexer
Short names:	ragel-d
Filenames:	*.rl
MIME types:	None
A lexer for Ragel in a D host file.

New in version 1.1.

class pygments.lexers.parsers.RagelEmbeddedLexer
Short names:	ragel-em
Filenames:	*.rl
MIME types:	None
A lexer for Ragel embedded in a host language file.

This will only highlight Ragel statements. If you want host language highlighting then call the language-specific Ragel lexer.

New in version 1.1.

class pygments.lexers.parsers.RagelJavaLexer
Short names:	ragel-java
Filenames:	*.rl
MIME types:	None
A lexer for Ragel in a Java host file.

New in version 1.1.

class pygments.lexers.parsers.RagelLexer
Short names:	ragel
Filenames:	None
MIME types:	None
A pure Ragel lexer. Use this for fragments of Ragel. For .rl files, use RagelEmbeddedLexer instead (or one of the language-specific subclasses).

New in version 1.1.

class pygments.lexers.parsers.RagelObjectiveCLexer
Short names:	ragel-objc
Filenames:	*.rl
MIME types:	None
A lexer for Ragel in an Objective C host file.

New in version 1.1.

class pygments.lexers.parsers.RagelRubyLexer
Short names:	ragel-ruby, ragel-rb
Filenames:	*.rl
MIME types:	None
A lexer for Ragel in a Ruby host file.

New in version 1.1.

class pygments.lexers.parsers.TreetopLexer
Short names:	treetop
Filenames:	*.treetop, *.tt
MIME types:	None
A lexer for Treetop grammars.

New in version 1.6.

Lexers for Pascal family languages

class pygments.lexers.pascal.AdaLexer
Short names:	ada, ada95, ada2005
Filenames:	*.adb, *.ads, *.ada
MIME types:	text/x-ada
For Ada source code.

New in version 1.3.

class pygments.lexers.pascal.DelphiLexer
Short names:	delphi, pas, pascal, objectpascal
Filenames:	*.pas
MIME types:	text/x-pascal
For Delphi (Borland Object Pascal), Turbo Pascal and Free Pascal source code.

Additional options accepted:

turbopascal
Highlight Turbo Pascal specific keywords (default: True).
delphi
Highlight Borland Delphi specific keywords (default: True).
freepascal
Highlight Free Pascal specific keywords (default: True).
units
A list of units that should be considered builtin, supported are System, SysUtils, Classes and Math. Default is to consider all of them builtin.
class pygments.lexers.pascal.Modula2Lexer
Short names:	modula2, m2
Filenames:	*.def, *.mod
MIME types:	text/x-modula2
For Modula-2 source code.

Additional options that determine which keywords are highlighted:

pim
Select PIM Modula-2 dialect (default: True).
iso
Select ISO Modula-2 dialect (default: False).
objm2
Select Objective Modula-2 dialect (default: False).
gm2ext
Also highlight GNU extensions (default: False).
New in version 1.3.

Lexers for the Pawn languages

class pygments.lexers.pawn.PawnLexer
Short names:	pawn
Filenames:	*.p, *.pwn, *.inc
MIME types:	text/x-pawn
For Pawn source code.

New in version 2.0.

class pygments.lexers.pawn.SourcePawnLexer
Short names:	sp
Filenames:	*.sp
MIME types:	text/x-sourcepawn
For SourcePawn source code with preprocessor directives.

New in version 1.6.

Lexers for Perl and related languages

class pygments.lexers.perl.Perl6Lexer
Short names:	perl6, pl6
Filenames:	*.pl, *.pm, *.nqp, *.p6, *.6pl, *.p6l, *.pl6, *.6pm, *.p6m, *.pm6, *.t
MIME types:	text/x-perl6, application/x-perl6
For Perl 6 source code.

New in version 2.0.

class pygments.lexers.perl.PerlLexer
Short names:	perl, pl
Filenames:	*.pl, *.pm, *.t
MIME types:	text/x-perl, application/x-perl
For Perl source code.

Lexers for PHP and related languages

class pygments.lexers.php.PhpLexer
Short names:	php, php3, php4, php5
Filenames:	*.php, *.php[345], *.inc
MIME types:	text/x-php
For PHP source code. For PHP embedded in HTML, use the HtmlPhpLexer.

Additional options accepted:

startinline
If given and True the lexer starts highlighting with php code (i.e.: no starting <?php required). The default is False.
funcnamehighlighting
If given and True, highlight builtin function names (default: True).
disabledmodules
If given, must be a list of module names whose function names should not be highlighted. By default all modules are highlighted except the special 'unknown' module that includes functions that are known to php but are undocumented.

To get a list of allowed modules have a look into the _php_builtins module:

>>> from pygments.lexers._php_builtins import MODULES
>>> MODULES.keys()
['PHP Options/Info', 'Zip', 'dba', ...]
In fact the names of those modules match the module names from the php documentation.

class pygments.lexers.php.ZephirLexer
Short names:	zephir
Filenames:	*.zep
MIME types:	None
For Zephir language source code.

Zephir is a compiled high level language aimed to the creation of C-extensions for PHP.

New in version 2.0.

Lexers for Prolog and Prolog-like languages

class pygments.lexers.prolog.LogtalkLexer
Short names:	logtalk
Filenames:	*.lgt, *.logtalk
MIME types:	text/x-logtalk
For Logtalk source code.

New in version 0.10.

class pygments.lexers.prolog.PrologLexer
Short names:	prolog
Filenames:	*.ecl, *.prolog, *.pro, *.pl
MIME types:	text/x-prolog
Lexer for Prolog files.

Lexers for Python and related languages

class pygments.lexers.python.CythonLexer
Short names:	cython, pyx, pyrex
Filenames:	*.pyx, *.pxd, *.pxi
MIME types:	text/x-cython, application/x-cython
For Pyrex and Cython source code.

New in version 1.1.

class pygments.lexers.python.DgLexer
Short names:	dg
Filenames:	*.dg
MIME types:	text/x-dg
Lexer for dg, a functional and object-oriented programming language running on the CPython 3 VM.

New in version 1.6.

class pygments.lexers.python.NumPyLexer
Short names:	numpy
Filenames:	None
MIME types:	None
A Python lexer recognizing Numerical Python builtins.

New in version 0.10.

class pygments.lexers.python.Python3Lexer
Short names:	python3, py3
Filenames:	None
MIME types:	text/x-python3, application/x-python3
For Python source code (version 3.0).

New in version 0.10.

class pygments.lexers.python.Python3TracebackLexer
Short names:	py3tb
Filenames:	*.py3tb
MIME types:	text/x-python3-traceback
For Python 3.0 tracebacks, with support for chained exceptions.

New in version 1.0.

class pygments.lexers.python.PythonConsoleLexer
Short names:	pycon
Filenames:	None
MIME types:	text/x-python-doctest
For Python console output or doctests, such as:

>>> a = 'foo'
>>> print a
foo
>>> 1 / 0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
Additional options:

python3
Use Python 3 lexer for code. Default is False.

New in version 1.0.

class pygments.lexers.python.PythonLexer
Short names:	python, py, sage
Filenames:	*.py, *.pyw, *.sc, SConstruct, SConscript, *.tac, *.sage
MIME types:	text/x-python, application/x-python
For Python source code.

class pygments.lexers.python.PythonTracebackLexer
Short names:	pytb
Filenames:	*.pytb
MIME types:	text/x-python-traceback
For Python tracebacks.

New in version 0.7.

Lexers for the R/S languages

class pygments.lexers.r.RConsoleLexer
Short names:	rconsole, rout
Filenames:	*.Rout
MIME types:	None
For R console transcripts or R CMD BATCH output files.

class pygments.lexers.r.RdLexer
Short names:	rd
Filenames:	*.Rd
MIME types:	text/x-r-doc
Pygments Lexer for R documentation (Rd) files

This is a very minimal implementation, highlighting little more than the macros. A description of Rd syntax is found in Writing R Extensions and Parsing Rd files.

New in version 1.6.

class pygments.lexers.r.SLexer
Short names:	splus, s, r
Filenames:	*.S, *.R, .Rhistory, .Rprofile, .Renviron
MIME types:	text/S-plus, text/S, text/x-r-source, text/x-r, text/x-R, text/x-r-history, text/x-r-profile
For S, S-plus, and R source code.

New in version 0.10.

Lexers for semantic web and RDF query languages and markup

class pygments.lexers.rdf.SparqlLexer
Short names:	sparql
Filenames:	*.rq, *.sparql
MIME types:	application/sparql-query
Lexer for SPARQL query language.

New in version 2.0.

Lexers for the REBOL and related languages

class pygments.lexers.rebol.RebolLexer
Short names:	rebol
Filenames:	*.r, *.r3, *.reb
MIME types:	text/x-rebol
A REBOL lexer.

New in version 1.1.

class pygments.lexers.rebol.RedLexer
Short names:	red, red/system
Filenames:	*.red, *.reds
MIME types:	text/x-red, text/x-red-system
A Red-language lexer.

New in version 2.0.

Lexer for resource definition files

class pygments.lexers.resource.ResourceLexer
Short names:	resource, resourcebundle
Filenames:	*.txt
MIME types:	None
Lexer for ICU Resource bundles.

New in version 2.0.

Lexer for Robot Framework

class pygments.lexers.robotframework.RobotFrameworkLexer
Short names:	robotframework
Filenames:	*.txt, *.robot
MIME types:	text/x-robotframework
For Robot Framework test data.

Supports both space and pipe separated plain text formats.

New in version 1.6.

Lexers for Ruby and related languages

class pygments.lexers.ruby.FancyLexer
Short names:	fancy, fy
Filenames:	*.fy, *.fancypack
MIME types:	text/x-fancysrc
Pygments Lexer For Fancy.

Fancy is a self-hosted, pure object-oriented, dynamic, class-based, concurrent general-purpose programming language running on Rubinius, the Ruby VM.

New in version 1.5.

class pygments.lexers.ruby.RubyConsoleLexer
Short names:	rbcon, irb
Filenames:	None
MIME types:	text/x-ruby-shellsession
For Ruby interactive console (irb) output like:

irb(main):001:0> a = 1
=> 1
irb(main):002:0> puts a
1
=> nil
class pygments.lexers.ruby.RubyLexer
Short names:	rb, ruby, duby
Filenames:	*.rb, *.rbw, Rakefile, *.rake, *.gemspec, *.rbx, *.duby
MIME types:	text/x-ruby, application/x-ruby
For Ruby source code.

Lexers for the Rust language

class pygments.lexers.rust.RustLexer
Short names:	rust
Filenames:	*.rs
MIME types:	text/x-rustsrc
Lexer for the Rust programming language (version 0.9).

New in version 1.6.

Lexer for scripting and embedded languages

class pygments.lexers.scripting.AppleScriptLexer
Short names:	applescript
Filenames:	*.applescript
MIME types:	None
For AppleScript source code, including AppleScript Studio. Contributed by Andreas Amann <aamann@mac.com>.

New in version 1.0.

class pygments.lexers.scripting.ChaiscriptLexer
Short names:	chai, chaiscript
Filenames:	*.chai
MIME types:	text/x-chaiscript, application/x-chaiscript
For ChaiScript source code.

New in version 2.0.

class pygments.lexers.scripting.HybrisLexer
Short names:	hybris, hy
Filenames:	*.hy, *.hyb
MIME types:	text/x-hybris, application/x-hybris
For Hybris source code.

New in version 1.4.

class pygments.lexers.scripting.LSLLexer
Short names:	lsl
Filenames:	*.lsl
MIME types:	text/x-lsl
For Second Life’s Linden Scripting Language source code.

New in version 2.0.

class pygments.lexers.scripting.LuaLexer
Short names:	lua
Filenames:	*.lua, *.wlua
MIME types:	text/x-lua, application/x-lua
For Lua source code.

Additional options accepted:

func_name_highlighting
If given and True, highlight builtin function names (default: True).
disabled_modules
If given, must be a list of module names whose function names should not be highlighted. By default all modules are highlighted.

To get a list of allowed modules have a look into the _lua_builtins module:

>>> from pygments.lexers._lua_builtins import MODULES
>>> MODULES.keys()
['string', 'coroutine', 'modules', 'io', 'basic', ...]
class pygments.lexers.scripting.MOOCodeLexer
Short names:	moocode, moo
Filenames:	*.moo
MIME types:	text/x-moocode
For MOOCode (the MOO scripting language).

New in version 0.9.

class pygments.lexers.scripting.MoonScriptLexer
Short names:	moon, moonscript
Filenames:	*.moon
MIME types:	text/x-moonscript, application/x-moonscript
For MoonScript source code.

New in version 1.5.

class pygments.lexers.scripting.RexxLexer
Short names:	rexx, arexx
Filenames:	*.rexx, *.rex, *.rx, *.arexx
MIME types:	text/x-rexx
Rexx is a scripting language available for a wide range of different platforms with its roots found on mainframe systems. It is popular for I/O- and data based tasks and can act as glue language to bind different applications together.

New in version 2.0.

Lexers for various shells

class pygments.lexers.shell.BashLexer
Short names:	bash, sh, ksh, shell
Filenames:	*.sh, *.ksh, *.bash, *.ebuild, *.eclass, .bashrc, bashrc, .bash\*, bash\*, PKGBUILD
MIME types:	application/x-sh, application/x-shellscript
Lexer for (ba|k|)sh shell scripts.

New in version 0.6.

class pygments.lexers.shell.BashSessionLexer
Short names:	console
Filenames:	*.sh-session
MIME types:	application/x-shell-session
Lexer for simplistic shell sessions.

New in version 1.1.

class pygments.lexers.shell.BatchLexer
Short names:	bat, batch, dosbatch, winbatch
Filenames:	*.bat, *.cmd
MIME types:	application/x-dos-batch
Lexer for the DOS/Windows Batch file format.

New in version 0.7.

class pygments.lexers.shell.PowerShellLexer
Short names:	powershell, posh, ps1, psm1
Filenames:	*.ps1, *.psm1
MIME types:	text/x-powershell
For Windows PowerShell code.

New in version 1.5.

class pygments.lexers.shell.ShellSessionLexer
Short names:	shell-session
Filenames:	*.shell-session
MIME types:	application/x-sh-session
Lexer for shell sessions that works with different command prompts

New in version 1.6.

class pygments.lexers.shell.TcshLexer
Short names:	tcsh, csh
Filenames:	*.tcsh, *.csh
MIME types:	application/x-csh
Lexer for tcsh scripts.

New in version 0.10.

Lexers for Smalltalk and related languages

class pygments.lexers.smalltalk.NewspeakLexer
Short names:	newspeak
Filenames:	*.ns2
MIME types:	text/x-newspeak
For Newspeak <http://newspeaklanguage.org/> syntax.

New in version 1.1.

class pygments.lexers.smalltalk.SmalltalkLexer
Short names:	smalltalk, squeak, st
Filenames:	*.st
MIME types:	text/x-smalltalk
For Smalltalk syntax. Contributed by Stefan Matthias Aust. Rewritten by Nils Winter.

New in version 0.10.

Lexers for the SNOBOL language

class pygments.lexers.snobol.SnobolLexer
Short names:	snobol
Filenames:	*.snobol
MIME types:	text/x-snobol
Lexer for the SNOBOL4 programming language.

Recognizes the common ASCII equivalents of the original SNOBOL4 operators. Does not require spaces around binary operators.

New in version 1.5.

Special lexers

class pygments.lexers.special.RawTokenLexer
Short names:	raw
Filenames:	None
MIME types:	application/x-pygments-tokens
Recreate a token stream formatted with the RawTokenFormatter. This lexer raises exceptions during parsing if the token stream in the file is malformed.

Additional options accepted:

compress
If set to "gz" or "bz2", decompress the token stream with the given compression algorithm before lexing (default: "").
class pygments.lexers.special.TextLexer
Short names:	text
Filenames:	*.txt
MIME types:	text/plain
“Null” lexer, doesn’t highlight anything.

Lexers for various SQL dialects and related interactive sessions

class pygments.lexers.sql.MySqlLexer
Short names:	mysql
Filenames:	None
MIME types:	text/x-mysql
Special lexer for MySQL.

class pygments.lexers.sql.PlPgsqlLexer
Short names:	plpgsql
Filenames:	None
MIME types:	text/x-plpgsql
Handle the extra syntax in Pl/pgSQL language.

New in version 1.5.

class pygments.lexers.sql.PostgresConsoleLexer
Short names:	psql, postgresql-console, postgres-console
Filenames:	None
MIME types:	text/x-postgresql-psql
Lexer for psql sessions.

New in version 1.5.

class pygments.lexers.sql.PostgresLexer
Short names:	postgresql, postgres
Filenames:	None
MIME types:	text/x-postgresql
Lexer for the PostgreSQL dialect of SQL.

New in version 1.5.

class pygments.lexers.sql.RqlLexer
Short names:	rql
Filenames:	*.rql
MIME types:	text/x-rql
Lexer for Relation Query Language.

RQL

New in version 2.0.

class pygments.lexers.sql.SqlLexer
Short names:	sql
Filenames:	*.sql
MIME types:	text/x-sql
Lexer for Structured Query Language. Currently, this lexer does not recognize any special syntax except ANSI SQL.

class pygments.lexers.sql.SqliteConsoleLexer
Short names:	sqlite3
Filenames:	*.sqlite3-console
MIME types:	text/x-sqlite3-console
Lexer for example sessions using sqlite3.

New in version 0.11.

Lexers for Tcl and related languages

class pygments.lexers.tcl.TclLexer
Short names:	tcl
Filenames:	*.tcl, *.rvt
MIME types:	text/x-tcl, text/x-script.tcl, application/x-tcl
For Tcl source code.

New in version 0.10.

Lexers for various template engines’ markup

class pygments.lexers.templates.CheetahHtmlLexer
Short names:	html+cheetah, html+spitfire, htmlcheetah
Filenames:	None
MIME types:	text/html+cheetah, text/html+spitfire
Subclass of the CheetahLexer that highlights unlexed data with the HtmlLexer.

class pygments.lexers.templates.CheetahJavascriptLexer
Short names:	js+cheetah, javascript+cheetah, js+spitfire, javascript+spitfire
Filenames:	None
MIME types:	application/x-javascript+cheetah, text/x-javascript+cheetah, text/javascript+cheetah, application/x-javascript+spitfire, text/x-javascript+spitfire, text/javascript+spitfire
Subclass of the CheetahLexer that highlights unlexed data with the JavascriptLexer.

class pygments.lexers.templates.CheetahLexer
Short names:	cheetah, spitfire
Filenames:	*.tmpl, *.spt
MIME types:	application/x-cheetah, application/x-spitfire
Generic cheetah templates lexer. Code that isn’t Cheetah markup is yielded as Token.Other. This also works for spitfire templates which use the same syntax.

class pygments.lexers.templates.CheetahXmlLexer
Short names:	xml+cheetah, xml+spitfire
Filenames:	None
MIME types:	application/xml+cheetah, application/xml+spitfire
Subclass of the CheetahLexer that highlights unlexed data with the XmlLexer.

class pygments.lexers.templates.ColdfusionCFCLexer
Short names:	cfc
Filenames:	*.cfc
MIME types:	None
Coldfusion markup/script components

New in version 2.0.

class pygments.lexers.templates.ColdfusionHtmlLexer
Short names:	cfm
Filenames:	*.cfm, *.cfml
MIME types:	application/x-coldfusion
Coldfusion markup in html

class pygments.lexers.templates.ColdfusionLexer
Short names:	cfs
Filenames:	None
MIME types:	None
Coldfusion statements

class pygments.lexers.templates.CssDjangoLexer
Short names:	css+django, css+jinja
Filenames:	None
MIME types:	text/css+django, text/css+jinja
Subclass of the DjangoLexer that highlights unlexed data with the CssLexer.

class pygments.lexers.templates.CssErbLexer
Short names:	css+erb, css+ruby
Filenames:	None
MIME types:	text/css+ruby
Subclass of ErbLexer which highlights unlexed data with the CssLexer.

class pygments.lexers.templates.CssGenshiLexer
Short names:	css+genshitext, css+genshi
Filenames:	None
MIME types:	text/css+genshi
A lexer that highlights CSS definitions in genshi text templates.

class pygments.lexers.templates.CssPhpLexer
Short names:	css+php
Filenames:	None
MIME types:	text/css+php
Subclass of PhpLexer which highlights unmatched data with the CssLexer.

class pygments.lexers.templates.CssSmartyLexer
Short names:	css+smarty
Filenames:	None
MIME types:	text/css+smarty
Subclass of the SmartyLexer that highlights unlexed data with the CssLexer.

class pygments.lexers.templates.DjangoLexer
Short names:	django, jinja
Filenames:	None
MIME types:	application/x-django-templating, application/x-jinja
Generic django and jinja template lexer.

It just highlights django/jinja code between the preprocessor directives, other data is left untouched by the lexer.

class pygments.lexers.templates.ErbLexer
Short names:	erb
Filenames:	None
MIME types:	application/x-ruby-templating
Generic ERB (Ruby Templating) lexer.

Just highlights ruby code between the preprocessor directives, other data is left untouched by the lexer.

All options are also forwarded to the RubyLexer.

class pygments.lexers.templates.EvoqueHtmlLexer
Short names:	html+evoque
Filenames:	*.html
MIME types:	text/html+evoque
Subclass of the EvoqueLexer that highlights unlexed data with the HtmlLexer.

New in version 1.1.

class pygments.lexers.templates.EvoqueLexer
Short names:	evoque
Filenames:	*.evoque
MIME types:	application/x-evoque
For files using the Evoque templating system.

New in version 1.1.

class pygments.lexers.templates.EvoqueXmlLexer
Short names:	xml+evoque
Filenames:	*.xml
MIME types:	application/xml+evoque
Subclass of the EvoqueLexer that highlights unlexed data with the XmlLexer.

New in version 1.1.

class pygments.lexers.templates.GenshiLexer
Short names:	genshi, kid, xml+genshi, xml+kid
Filenames:	*.kid
MIME types:	application/x-genshi, application/x-kid
A lexer that highlights genshi and kid kid XML templates.

class pygments.lexers.templates.GenshiTextLexer
Short names:	genshitext
Filenames:	None
MIME types:	application/x-genshi-text, text/x-genshi
A lexer that highlights genshi text templates.

class pygments.lexers.templates.HandlebarsHtmlLexer
Short names:	html+handlebars
Filenames:	*.handlebars, *.hbs
MIME types:	text/html+handlebars, text/x-handlebars-template
Subclass of the HandlebarsLexer that highlights unlexed data with the HtmlLexer.

New in version 2.0.

class pygments.lexers.templates.HandlebarsLexer
Short names:	handlebars
Filenames:	None
MIME types:	None
Generic handlebars <http://handlebarsjs.com/> template lexer.

Highlights only the Handlebars template tags (stuff between {{ and }}). Everything else is left for a delegating lexer.

New in version 2.0.

class pygments.lexers.templates.HtmlDjangoLexer
Short names:	html+django, html+jinja, htmldjango
Filenames:	None
MIME types:	text/html+django, text/html+jinja
Subclass of the DjangoLexer that highlights unlexed data with the HtmlLexer.

Nested Javascript and CSS is highlighted too.

class pygments.lexers.templates.HtmlGenshiLexer
Short names:	html+genshi, html+kid
Filenames:	None
MIME types:	text/html+genshi
A lexer that highlights genshi and kid kid HTML templates.

class pygments.lexers.templates.HtmlPhpLexer
Short names:	html+php
Filenames:	*.phtml
MIME types:	application/x-php, application/x-httpd-php, application/x-httpd-php3, application/x-httpd-php4, application/x-httpd-php5
Subclass of PhpLexer that highlights unhandled data with the HtmlLexer.

Nested Javascript and CSS is highlighted too.

class pygments.lexers.templates.HtmlSmartyLexer
Short names:	html+smarty
Filenames:	None
MIME types:	text/html+smarty
Subclass of the SmartyLexer that highlights unlexed data with the HtmlLexer.

Nested Javascript and CSS is highlighted too.

class pygments.lexers.templates.JavascriptDjangoLexer
Short names:	js+django, javascript+django, js+jinja, javascript+jinja
Filenames:	None
MIME types:	application/x-javascript+django, application/x-javascript+jinja, text/x-javascript+django, text/x-javascript+jinja, text/javascript+django, text/javascript+jinja
Subclass of the DjangoLexer that highlights unlexed data with the JavascriptLexer.

class pygments.lexers.templates.JavascriptErbLexer
Short names:	js+erb, javascript+erb, js+ruby, javascript+ruby
Filenames:	None
MIME types:	application/x-javascript+ruby, text/x-javascript+ruby, text/javascript+ruby
Subclass of ErbLexer which highlights unlexed data with the JavascriptLexer.

class pygments.lexers.templates.JavascriptGenshiLexer
Short names:	js+genshitext, js+genshi, javascript+genshitext, javascript+genshi
Filenames:	None
MIME types:	application/x-javascript+genshi, text/x-javascript+genshi, text/javascript+genshi
A lexer that highlights javascript code in genshi text templates.

class pygments.lexers.templates.JavascriptPhpLexer
Short names:	js+php, javascript+php
Filenames:	None
MIME types:	application/x-javascript+php, text/x-javascript+php, text/javascript+php
Subclass of PhpLexer which highlights unmatched data with the JavascriptLexer.

class pygments.lexers.templates.JavascriptSmartyLexer
Short names:	js+smarty, javascript+smarty
Filenames:	None
MIME types:	application/x-javascript+smarty, text/x-javascript+smarty, text/javascript+smarty
Subclass of the SmartyLexer that highlights unlexed data with the JavascriptLexer.

class pygments.lexers.templates.JspLexer
Short names:	jsp
Filenames:	*.jsp
MIME types:	application/x-jsp
Lexer for Java Server Pages.

New in version 0.7.

class pygments.lexers.templates.LassoCssLexer
Short names:	css+lasso
Filenames:	None
MIME types:	text/css+lasso
Subclass of the LassoLexer which highlights unhandled data with the CssLexer.

New in version 1.6.

class pygments.lexers.templates.LassoHtmlLexer
Short names:	html+lasso
Filenames:	None
MIME types:	text/html+lasso, application/x-httpd-lasso, application/x-httpd-lasso[89]
Subclass of the LassoLexer which highlights unhandled data with the HtmlLexer.

Nested JavaScript and CSS is also highlighted.

New in version 1.6.

class pygments.lexers.templates.LassoJavascriptLexer
Short names:	js+lasso, javascript+lasso
Filenames:	None
MIME types:	application/x-javascript+lasso, text/x-javascript+lasso, text/javascript+lasso
Subclass of the LassoLexer which highlights unhandled data with the JavascriptLexer.

New in version 1.6.

class pygments.lexers.templates.LassoXmlLexer
Short names:	xml+lasso
Filenames:	None
MIME types:	application/xml+lasso
Subclass of the LassoLexer which highlights unhandled data with the XmlLexer.

New in version 1.6.

class pygments.lexers.templates.LiquidLexer
Short names:	liquid
Filenames:	*.liquid
MIME types:	None
Lexer for Liquid templates.

New in version 2.0.

class pygments.lexers.templates.MakoCssLexer
Short names:	css+mako
Filenames:	None
MIME types:	text/css+mako
Subclass of the MakoLexer that highlights unlexed data with the CssLexer.

New in version 0.7.

class pygments.lexers.templates.MakoHtmlLexer
Short names:	html+mako
Filenames:	None
MIME types:	text/html+mako
Subclass of the MakoLexer that highlights unlexed data with the HtmlLexer.

New in version 0.7.

class pygments.lexers.templates.MakoJavascriptLexer
Short names:	js+mako, javascript+mako
Filenames:	None
MIME types:	application/x-javascript+mako, text/x-javascript+mako, text/javascript+mako
Subclass of the MakoLexer that highlights unlexed data with the JavascriptLexer.

New in version 0.7.

class pygments.lexers.templates.MakoLexer
Short names:	mako
Filenames:	*.mao
MIME types:	application/x-mako
Generic mako templates lexer. Code that isn’t Mako markup is yielded as Token.Other.

New in version 0.7.

class pygments.lexers.templates.MakoXmlLexer
Short names:	xml+mako
Filenames:	None
MIME types:	application/xml+mako
Subclass of the MakoLexer that highlights unlexed data with the XmlLexer.

New in version 0.7.

class pygments.lexers.templates.MasonLexer
Short names:	mason
Filenames:	*.m, *.mhtml, *.mc, *.mi, autohandler, dhandler
MIME types:	application/x-mason
Generic mason templates lexer. Stolen from Myghty lexer. Code that isn’t Mason markup is HTML.

New in version 1.4.

class pygments.lexers.templates.MyghtyCssLexer
Short names:	css+myghty
Filenames:	None
MIME types:	text/css+myghty
Subclass of the MyghtyLexer that highlights unlexed data with the CssLexer.

New in version 0.6.

class pygments.lexers.templates.MyghtyHtmlLexer
Short names:	html+myghty
Filenames:	None
MIME types:	text/html+myghty
Subclass of the MyghtyLexer that highlights unlexed data with the HtmlLexer.

New in version 0.6.

class pygments.lexers.templates.MyghtyJavascriptLexer
Short names:	js+myghty, javascript+myghty
Filenames:	None
MIME types:	application/x-javascript+myghty, text/x-javascript+myghty, text/javascript+mygthy
Subclass of the MyghtyLexer that highlights unlexed data with the JavascriptLexer.

New in version 0.6.

class pygments.lexers.templates.MyghtyLexer
Short names:	myghty
Filenames:	*.myt, autodelegate
MIME types:	application/x-myghty
Generic myghty templates lexer. Code that isn’t Myghty markup is yielded as Token.Other.

New in version 0.6.

class pygments.lexers.templates.MyghtyXmlLexer
Short names:	xml+myghty
Filenames:	None
MIME types:	application/xml+myghty
Subclass of the MyghtyLexer that highlights unlexed data with the XmlLexer.

New in version 0.6.

class pygments.lexers.templates.RhtmlLexer
Short names:	rhtml, html+erb, html+ruby
Filenames:	*.rhtml
MIME types:	text/html+ruby
Subclass of the ERB lexer that highlights the unlexed data with the html lexer.

Nested Javascript and CSS is highlighted too.

class pygments.lexers.templates.SmartyLexer
Short names:	smarty
Filenames:	*.tpl
MIME types:	application/x-smarty
Generic Smarty template lexer.

Just highlights smarty code between the preprocessor directives, other data is left untouched by the lexer.

class pygments.lexers.templates.SspLexer
Short names:	ssp
Filenames:	*.ssp
MIME types:	application/x-ssp
Lexer for Scalate Server Pages.

New in version 1.4.

class pygments.lexers.templates.TeaTemplateLexer
Short names:	tea
Filenames:	*.tea
MIME types:	text/x-tea
Lexer for Tea Templates.

New in version 1.5.

class pygments.lexers.templates.TwigHtmlLexer
Short names:	html+twig
Filenames:	*.twig
MIME types:	text/html+twig
Subclass of the TwigLexer that highlights unlexed data with the HtmlLexer.

New in version 2.0.

class pygments.lexers.templates.TwigLexer
Short names:	twig
Filenames:	None
MIME types:	application/x-twig
Twig template lexer.

It just highlights Twig code between the preprocessor directives, other data is left untouched by the lexer.

New in version 2.0.

class pygments.lexers.templates.VelocityHtmlLexer
Short names:	html+velocity
Filenames:	None
MIME types:	text/html+velocity
Subclass of the VelocityLexer that highlights unlexed data with the HtmlLexer.

class pygments.lexers.templates.VelocityLexer
Short names:	velocity
Filenames:	*.vm, *.fhtml
MIME types:	None
Generic Velocity template lexer.

Just highlights velocity directives and variable references, other data is left untouched by the lexer.

class pygments.lexers.templates.VelocityXmlLexer
Short names:	xml+velocity
Filenames:	None
MIME types:	application/xml+velocity
Subclass of the VelocityLexer that highlights unlexed data with the XmlLexer.

class pygments.lexers.templates.XmlDjangoLexer
Short names:	xml+django, xml+jinja
Filenames:	None
MIME types:	application/xml+django, application/xml+jinja
Subclass of the DjangoLexer that highlights unlexed data with the XmlLexer.

class pygments.lexers.templates.XmlErbLexer
Short names:	xml+erb, xml+ruby
Filenames:	None
MIME types:	application/xml+ruby
Subclass of ErbLexer which highlights data outside preprocessor directives with the XmlLexer.

class pygments.lexers.templates.XmlPhpLexer
Short names:	xml+php
Filenames:	None
MIME types:	application/xml+php
Subclass of PhpLexer that highlights unhandled data with the XmlLexer.

class pygments.lexers.templates.XmlSmartyLexer
Short names:	xml+smarty
Filenames:	None
MIME types:	application/xml+smarty
Subclass of the SmartyLexer that highlights unlexed data with the XmlLexer.

class pygments.lexers.templates.YamlJinjaLexer
Short names:	yaml+jinja, salt, sls
Filenames:	*.sls
MIME types:	text/x-yaml+jinja, text/x-sls
Subclass of the DjangoLexer that highlights unlexed data with the YamlLexer.

Commonly used in Saltstack salt states.

New in version 2.0.

Lexers for testing languages

class pygments.lexers.testing.GherkinLexer
Short names:	cucumber, gherkin
Filenames:	*.feature
MIME types:	text/x-gherkin
For Gherkin <http://github.com/aslakhellesoy/gherkin/> syntax.

New in version 1.2.

Lexers for languages related to text processing

class pygments.lexers.textedit.AwkLexer
Short names:	awk, gawk, mawk, nawk
Filenames:	*.awk
MIME types:	application/x-awk
For Awk scripts.

New in version 1.5.

class pygments.lexers.textedit.VimLexer
Short names:	vim
Filenames:	*.vim, .vimrc, .exrc, .gvimrc, vimrc, exrc, gvimrc, vimrc, gvimrc
MIME types:	text/x-vim
Lexer for VimL script files.

New in version 0.8.

Lexers for various text formats

class pygments.lexers.textfmts.GettextLexer
Short names:	pot, po
Filenames:	*.pot, *.po
MIME types:	application/x-gettext, text/x-gettext, text/gettext
Lexer for Gettext catalog files.

New in version 0.9.

class pygments.lexers.textfmts.HttpLexer
Short names:	http
Filenames:	None
MIME types:	None
Lexer for HTTP sessions.

New in version 1.5.

class pygments.lexers.textfmts.IrcLogsLexer
Short names:	irc
Filenames:	*.weechatlog
MIME types:	text/x-irclog
Lexer for IRC logs in irssi, xchat or weechat style.

class pygments.lexers.textfmts.TodotxtLexer
Short names:	todotxt
Filenames:	todo.txt, *.todotxt
MIME types:	text/x-todo
Lexer for Todo.txt todo list format.

New in version 2.0.

Lexers for theorem-proving languages

class pygments.lexers.theorem.CoqLexer
Short names:	coq
Filenames:	*.v
MIME types:	text/x-coq
For the Coq theorem prover.

New in version 1.5.

class pygments.lexers.theorem.IsabelleLexer
Short names:	isabelle
Filenames:	*.thy
MIME types:	text/x-isabelle
For the Isabelle proof assistant.

New in version 2.0.

class pygments.lexers.theorem.LeanLexer
Short names:	lean
Filenames:	*.lean
MIME types:	text/x-lean
For the Lean theorem prover.

New in version 2.0.

Lexers for UrbiScript language

class pygments.lexers.urbi.UrbiscriptLexer
Short names:	urbiscript
Filenames:	*.u
MIME types:	application/x-urbiscript
For UrbiScript source code.

New in version 1.5.

Lexers for misc. web stuff

class pygments.lexers.webmisc.CirruLexer
Short names:	cirru
Filenames:	*.cirru
MIME types:	text/x-cirru
Syntax rules of Cirru can be found at: http://cirru.org/

using () to markup blocks, but limited in the same line
using "" to markup strings, allow \ to escape
using $ as a shorthand for () till indentation end or )
using indentations for create nesting
New in version 2.0.

class pygments.lexers.webmisc.DuelLexer
Short names:	duel, jbst, jsonml+bst
Filenames:	*.duel, *.jbst
MIME types:	text/x-duel, text/x-jbst
Lexer for Duel Views Engine (formerly JBST) markup with JavaScript code blocks. See http://duelengine.org/. See http://jsonml.org/jbst/.

New in version 1.4.

class pygments.lexers.webmisc.QmlLexer
Short names:	qml
Filenames:	*.qml
MIME types:	application/x-qml
For QML files. See http://doc.qt.digia.com/4.7/qdeclarativeintroduction.html.

New in version 1.6.

class pygments.lexers.webmisc.SlimLexer
Short names:	slim
Filenames:	*.slim
MIME types:	text/x-slim
For Slim markup.

New in version 2.0.

class pygments.lexers.webmisc.XQueryLexer
Short names:	xquery, xqy, xq, xql, xqm
Filenames:	*.xqy, *.xquery, *.xq, *.xql, *.xqm
MIME types:	text/xquery, application/xquery
An XQuery lexer, parsing a stream and outputting the tokens needed to highlight xquery code.

New in version 1.4.
{% endhighlight %}
