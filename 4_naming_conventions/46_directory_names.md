<!--- @file
  4.6 Directory Names

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

## 4.6 Directory Names
Below sections are the directory naming guidelines for EDK II modules

#### 4.6.1 EDKII package directory

```
<PackageName>Pkg

   <PackageName> REQUIRED  *
```

#### 4.6.2 EDKII Module directory

* If the implementation supports >=2 or all CPU archs:
```
<ModuleName><Phase>

   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm, StandaloneMm, Smm,
                              Uefi.
   <ModuleName>   REQUIRED    *

Example:
   CpuDxe/
```

* If the implementation is for the specific CPU arch or vendor:
```
<ModuleName><Phase><CpuArch><Vendor>

   <ModuleName>   REQUIRED    * 
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm,
                              StandaloneMm, Smm, Uefi.
   <CpuArch>      OPTIONAL    Ia32, X64, Arm, AArch64, RiscV64, LoongArch64, Ebc, X86
                              (X86 implies Ia32 and X64).
   <Vendor>       OPTIONAL    *

Example:
   CpuDxeRiscv64/
```

* If the implementation does not have any shared code between phases (e.g.
MdeModulePkg/Universal/PCD) and supports >=2 or all CPU archs:

```
<Feature>/<Phase>

   <Feature>      OPTIONAL    *
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm, StandaloneMm, Smm,
                              Uefi.

Example:
   Pcd/Dxe/
```

* If the implementation does not have any shared code between phases (e.g.
MdeModulePkg/Universal/PCD) and is for the specifc CPU arch or vendor:
```
<Feature>/<Phase>/<CpuArch>/<Vendor>

   <Feature>      OPTIONAL    *
   <Phase>        REQUIRED    Base, Sec, Pei, Dxe, DxeRuntime, Mm, StandaloneMm, Smm,
                              Uefi.
   <CpuArch>      OPTIONAL    Ia32, X64, Arm, AArch64, RiscV64, LoongArch64, Ebc, X86
                              (X86 implies Ia32 and X64).
   <Vendor>       OPTIONAL    *
```

#### 4.6.2 EDKII Library directory
```
<Phase><CpuArch><Vendor><LibraryClassName><Dependency>

   <Phase>              REQUIRED     Base, Sec, Pei, Dxe, DxeRuntime, Mm,
                                     StandaloneMm, Smm, Uefi.
   <CpuArch>            OPTIONAL     Ia32, X64, Arm, AArch64, RiscV64, LoongArch64,
                                     Ebc, X86 (X86 implies Ia32 and X64).
   <Vendor>             OPTIONAL     *
   <LibraryClassName>   REQUIRED     *
   <Dependency>         OPTIONAL     * (Typically name of PPI, Protocol, LibraryClass
                                       that the implementation is layered on top of).

Example:
   SmmAmdSmmCpuFeaturesLib/
```
