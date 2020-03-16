# (Your DIP title)

| Field           | Value                                                           |
|-----------------|-----------------------------------------------------------------|
| DIP:            | (number/id -- assigned by DIP Manager)                          |
| Review Count:   | 0 (edited by DIP Manager)                                       |
| Author:         | Florian (moonlightsentinel@disroot.org)                  |
| Implementation: | (links to implementation PR if any)                             |
| Status:         | Will be set by the DIP manager (e.g. "Approved" or "Rejected")  |

## Abstract

[comment]: # (Required: Short and concise description of the idea in a few lines.)

Allow combination and grouping of multiple version identifiers within a single `version` statement.

## Contents
* [Rationale](#rationale)
* [Prior Work](#prior-work)
* [Description](#description)
* [Breaking Changes and Deprecations](#breaking-changes-and-deprecations)
* [Reference](#reference)
* [Copyright & License](#copyright--license)
* [Reviews](#reviews)

## Rationale

[comment]: # (  Required: )
[comment]: # (  A short motivation about the importance and benefits of the proposed change.  An existing,    )
[comment]: # (  well-known issue or a use case for an existing projects can greatly increase the    )
[comment]: # (  chances of the DIP being understood and carefully evaluated.    )

[Predefined versions](https://dlang.org/spec/version.html#predefined-versions) (as well as
user-defined versions) allow programmers to customize their code according to certain
criterias:

- architecture (`Posix`, `Windows`)
- compiler (`GNU`, `LDC`)
- availiable features (`D_AVX`, `D_Exceptions`)
- production builds, e.g. containing extended logging outputs (`Log`)
- ...

These conditions are not mutually exclusive and can be combined to target specific scenarios, e.g. when compiling for `Windows` using `LDC` or relying on inline assembly identified by `D_InlineAsm_X86` or `D_InlineAsm_X86_64`.
D currently lacks a concise way to express this which leads to akward workarounds demostrated by the following examples.

The following example taken from DRuntimes [`osthread.d`](https://github.com/dlang/druntime/blob/master/src/core/thread/osthread.d) illustrates a pattern commonly used in plattform-specific bindings where similar targets are conflated and treated equally.
This is achieved by introducing a common identifier which is defined for every plattform specific (and mutually exclusive) identifier:

```D
version (OSX)
    version = Darwin;
else version (iOS)
    version = Darwin;
else version (TVOS)
    version = Darwin;
else version (WatchOS)
    version = Darwin;

version(Darwin)
{
    // ...
}
```


## Prior Work

[comment]: # (  Required.   )

[comment]: # (  If the proposed feature exists, or has been proposed, in other languages, this is the place )
[comment]: # (  to provide the details of those implementations and proposals. Ditto for prior DIPs.    )

[comment]: # (  If there is no prior work to be found, it must be explicitly noted here.    )

No known.

## Description

[comment]: # (  Required.   )

[comment]: # (  Detailed technical description of the new semantics. Language grammar changes   )
[comment]: # (  per https://dlang.org/spec/grammar.html needed to support the new syntax  )
[comment]: # (  or change must be mentioned. Examples demonstrating the new semantics will    )
[comment]: # (  strengthen the proposal and should be considered mandatory. )

## Breaking Changes and Deprecations

[comment]: # (  This section is not required if no breaking changes or deprecations are anticipated.    )

[comment]: # (  Provide a detailed analysis on how the proposed changes may affect existing )
[comment]: # (  user code and a step-by-step explanation of the deprecation process which is    )
[comment]: # (  supposed to handle breakage in a non-intrusive manner. Changes that may break   )
[comment]: # (  user code and have no well-defined deprecation process have a minimal chance of )
[comment]: # (  being approved. )

## Reference
[comment]: # (  Optional links to reference material such as existing discussions, research papers  )
[comment]: # (  or any other supplementary materials.   )

[math]: https://github.com/dlang/phobos/blob/master/std/math.d
[math_or]: https://github.com/dlang/phobos/blob/f8196e626feeb4f970e93cc94aecf1f24976f904/std/math.d#L146
[math_and]: https://github.com/dlang/phobos/blob/f8196e626feeb4f970e93cc94aecf1f24976f904/std/math.d#L124

[osthread_or]: https://github.com/dlang/druntime/blob/4cf0be96863d6803e1fc30f46fee99a0788966d1/src/core/thread/osthread.d#L22
[osthread_and]:

## Copyright & License
Copyright (c) 2019 by the D Language Foundation

Licensed under [Creative Commons Zero 1.0](https://creativecommons.org/publicdomain/zero/1.0/legalcode.txt)

## Reviews
The DIP Manager will supplement this section with a summary of each review stage
of the DIP process beyond the Draft Review.
