# Third-party notices

RigCanvas is freeware by vitcox (see LICENSE.txt). It is an independent project and is not affiliated with or endorsed by Thermalright.

## Bundled

| Component | License | Notes |
|---|---|---|
| **LibreHardwareMonitorLib** 0.9.6 | Mozilla Public License 2.0 | Used unmodified. Source code: https://github.com/LibreHardwareMonitor/LibreHardwareMonitor · License: https://www.mozilla.org/MPL/2.0/ |
| **HidSharp** 2.6.4 (used by LibreHardwareMonitorLib) | Apache License 2.0 | © 2010-2025 James F. Bellinger. Full license text: `licenses/HidSharp-LICENSE.txt` |
| **System.Management**, **System.IO.Ports** (used by LibreHardwareMonitorLib) | MIT | © .NET Foundation and contributors. https://github.com/dotnet/runtime |
| **.NET runtime** and **Windows SDK projection** (self-contained build) | MIT | © .NET Foundation and contributors / © Microsoft Corporation. https://github.com/dotnet/runtime · https://github.com/microsoft/CsWinRT |

The MIT License (for the components marked MIT above):

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Used at runtime, not bundled

- **PawnIO** (kernel driver LibreHardwareMonitor uses for CPU / motherboard sensors) — © namazso. Must be installed separately from https://pawnio.eu/.
- **Thermalright TRCC** (optional: fallback `USBLCDNEW.exe` screen driver, `HWINFO.exe`) — © Thermalright. Proprietary; not required.
- **HWiNFO** (optional, shipped inside TRCC) — © REALiX s.r.o.
- **RivaTuner Statistics Server** (optional, for game FPS) — © Guru3D / Unwinder.
- **Open-Meteo** (optional weather data, fetched over the internet) — https://open-meteo.com/, data under CC BY 4.0.

The LCD protocol and shared-memory layout were reverse engineered for interoperability with hardware the user owns.