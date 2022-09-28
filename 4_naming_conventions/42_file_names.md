<!--- @file
  4.2 File Names

  Copyright (c) 2006-2017, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

## 4.2 File Names

### 4.2.1 There is no limit to file name lengths.

Do not assume that file names must be 8.3 compatible. Be reasonable though. Let
the file names be as long as necessary, but no longer. Some operating systems
limit file names to 32 characters.

### 4.2.2 Spaces in file and directory names are NOT permitted.

Allowing spaces would cause problems with certain versions of existing industry
tools and does not provide additional clarity.

### 4.2.3 Never start file names with numbers.

Most source control systems will not be able to handle file names that start
with numbers.

### 4.2.4 Non-standard characters shall not occur in file names.

All file names within an EDK II source tree must comply with the following
regular expression:

```
[A-Za-z][_A-Za-z0-9-]*[A-Za-z0-9]+
```

That is, a letter followed by zero, or more, letters, underscores, dashes, or
digits followed by a period followed by one or more letters or digits.

### 4.2.5 File naming guidelines for modules

Below sections are the file naming guidelines for EDK II meta files and source files.

#### 4.2.5.1 EDK II meta files within a package

```
<PackageName>Pkg.dec
<PackageName>Pkg.dsc

   <PackageName> REQUIRED  *
```

#### 4.2.5.2 EDK II INF file within a Module instance
* If the implementation supports >=2 or all CPU archs:
```
<ModuleName><Phase>.inf

   <ModuleName>   REQUIRED    *
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm, StandaloneMm,
                              Smm, Uefi.

Example:
   CpuIo2Dxe.inf
```

* If the implementation of CPU arch or vendor shares some code in the module. Or the implementation is only for the specific CPU arch or vendor.
```
<ModuleName><Phase><CpuArch><Vendor>.inf

   <ModuleName>   REQUIRED    *
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm,
                              StandaloneMm, Smm, Uefi.
   <CpuArch>      OPTIONAL    Ia32, X64, Arm, AArch64, RiscV64, LoongArch64, Ebc, X86
                              (X86 implies Ia32 and X64).
   <Vendor>       OPTIONAL    *

Example:
   CpuIo2DxeAmd.inf
```

If the implementation does not have any shared code between phases. The module INF is located under \<Feature\>/\<Phase\> or \<Feature\>/<Phase\>/<CpuArch\>/<Vendor\> (see section 4.6 Directory Names).

* If the implementation supports >=2 or all CPU archs:
```
<Feature>/<Phase>/<ModuleName>.inf

   <Feature>      OPTIONAL    *
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm, StandaloneMm, Smm,
                              Uefi.
   <ModuleName>   REQUIRED    Same as <Feature>

Example:
   PCD/Dxe/Pcd.inf
```

* If the implementation of CPU arch or vendor shares some code in the module. Or the implementation is only for the specific CPU arch or vendor.
```
<Feature>/<Phase>/<ModuleName><CpuArch><Vendor>.inf

   <Feature>      OPTIONAL    *
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm, StandaloneMm, Smm,
                              Uefi.
   <CpuArch>      OPTIONAL    Ia32, X64, Arm, AArch64, RiscV64, LoongArch64, Ebc, X86
                              (X86 implies Ia32 and X64).
   <Vendor>       OPTIONAL    *
   <ModuleName>   REQUIRED    Same as <Feature>

```
#### 4.2.5.3 EDK II INF file within a Library instance
```
<Phase><CpuArch><Vendor><LibraryClassName><Dependency>.inf
   <Phase>              REQUIRED     Base, Sec, Pei, Dxe, DxeRuntime, Mm,
                                     StandaloneMm, Smm, Uefi.
   <CpuArch>            OPTIONAL     Ia32, X64, Arm, AArch64, RiscV64, LoongArch64,
                                     Ebc, X86 (X86 implies Ia32 and X64).
   <Vendor>             OPTIONAL     *
   <LibraryClassName>   REQUIRED     *
   <Dependency>         OPTIONAL     * (Typically name of PPI, Protocol, LibraryClass
                                       that the implementation is layered on top of)

Example:
   SmmAmdSmmCpuFeaturesLib.inf
   SmmIntelSmmCpuFeaturesLib.inf
```

#### 4.2.5.4 EDK II source files within a Library/Module instance

```
<FileName>.c
<FileName>.h
<CpuArch><Vendor><FileName>.c
<CpuArch><Vendor><FileName>.h
<CpuArch>/<FileName>.c
<CpuArch>/<FileName>.h
<CpuArch>/<FileName>.nasm
<CpuArch>/<FileName>.S
<CpuArch>/<Vendor>/<FileName>.c
<CpuArch>/<Vendor>/<FileName>.h
<CpuArch>/<Vendor>/<FileName>.nasm
<CpuArch>/<Vendor>/<FileName>.S

   <CpuArch> OPTIONAL   Ia32, X64, Arm, AArch64, RiscV64, LoongArch64, Ebc, X86
                        (X86 implies Ia32 and X64).
   <Vendor>  OPTIONAL   *

Example:
   IA32/SmiException.nasm
   X64/SmiException.nasm
   SmmCpuFeatureLib.c
   SmmCpuFeatureLibCommon.c
   IntelSmmCpuFeaturesLib.c
   AmdSmmCpuFeaturesLib.c

   Or,
   X86/IA32/SmiException.nasm
   X86/X64/SmiException.nasm
   X86/IntelSmmCpuFeaturesLib.c
   X86/AmdSmmCpuFeaturesLib.c
   RiscV64/JustAnExampleLib.c
   SmmCpuFeatureLib.c
   SmmCpuFeatureLibCommon.c
```
