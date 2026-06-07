<div align="center">

# Mohammed EL Kadiri

**Systems Software Engineer · Kernel Development · Security Hardening**

Systems software engineer focused on kernel development, operating system internals, and security hardening.
Currently contributing to the Linux kernel and building production-grade systems components in C/C++17.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohammedelkadiri/)
[![Medium](https://img.shields.io/badge/Medium-000000?style=flat&logo=medium&logoColor=white)](https://medium.com/@medelkadiri)
[![Linux Kernel](https://img.shields.io/badge/Linux_Kernel-Contributor-FCC624?style=flat&logo=linux&logoColor=black)](https://lore.kernel.org/all/?q=from%3Amed08elkadiri%40gmail.com)

</div>

---

### What This GitHub Contains

This is my systems engineering workspace. The projects here deal with the lowest layers of software, the code that sits between hardware and applications. File descriptors, memory allocators, thread synchronization, shell interpreters, and kernel patches. If you are not familiar with systems programming: this is the code that makes operating systems like Linux and macOS work reliably, securely, and fast.

---

### What I Build

<table>
<tr>
<td width="50%">

**[systems-engineering](https://github.com/medelkadiri/systems-engineering)**

Production-grade C++17 systems components with security hardening, benchmarking, and cross-platform support.

`RAII fd wrapper` · `lock-free stack` · `memory pool` · `thread pool` · `ring buffer`

![C++17](https://img.shields.io/badge/C++17-00599C?style=flat&logo=cplusplus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat&logo=apple&logoColor=white)

</td>
<td width="50%">

**[jakashell](https://github.com/medelkadiri/jakashell)**

High-performance Linux shell with zero-copy IPC via mmap, CPU-affinity scheduling, and eBPF-based telemetry.

`mmap IPC` · `CPU affinity` · `eBPF tracing` · `process management`

![C](https://img.shields.io/badge/C-A8B9CC?style=flat&logo=c&logoColor=black)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![eBPF](https://img.shields.io/badge/eBPF-FF6600?style=flat)

</td>
</tr>
<tr>
<td colspan="2" align="center">

**[Linux Kernel Contributions](https://lore.kernel.org/all/?q=from%3Amed08elkadiri%40gmail.com)**

Upstream patches to the Linux kernel. Current focus: slab allocator security hardening against cross-cache heap exploitation.

![Kernel](https://img.shields.io/badge/Linux_Kernel-6.17-FCC624?style=flat&logo=linux&logoColor=black)

</td>
</tr>
</table>

---

<!-- KERNEL_PATCHES_START -->

### Linux Kernel Patches

<div align="center">

*Upstream contributions to the Linux kernel — tracked from [lore.kernel.org](https://lore.kernel.org/all/?q=from%3Amed08elkadiri%40gmail.com)*

</div>

<br>

<table>
<tr>
<th align="center">#</th>
<th>Patch</th>
<th>Subsystem</th>
<th>Status</th>
<th>Date</th>
</tr>
<tr>
<td align="center"><code>5</code></td>
<td><a href="https://lore.kernel.org/all/20260606155856.15548-1-med08elkadiri@gmail.com/"><b>docs/mm: document slab cache isolation with SLAB_NO_MERGE</b></a><br><sub>Document when and how to use SLAB_NO_MERGE to protect security-critical slab caches from cross-cache heap exploitation.</sub></td>
<td><code>Documentation/mm</code></td>
<td><img src="https://img.shields.io/badge/Submitted-2196F3?style=flat-square" /></td>
<td><sub>06/06/2026</sub></td>
</tr>
<tr>
<td align="center"><code>4</code></td>
<td><a href="https://lore.kernel.org/all/20260606142558.13809-1-med08elkadiri@gmail.com/"><b>cred: prevent slab cache merging for cred_jar</b></a><br><sub>Add SLAB_NO_MERGE to isolate struct cred (uid, gid, capabilities) from cross-cache heap attacks.</sub></td>
<td><code>kernel/cred</code></td>
<td><img src="https://img.shields.io/badge/Submitted-2196F3?style=flat-square" /></td>
<td><sub>06/06/2026</sub></td>
</tr>
<tr>
<td align="center"><code>3</code></td>
<td><a href="https://lore.kernel.org/all/20260604125034.13757-1-med08elkadiri@gmail.com/"><b>keys: prevent slab cache merging for key_jar</b></a><br><sub>Add SLAB_NO_MERGE to isolate struct key from cross-cache heap attacks.</sub><br><sub>Acked-by: Vlastimil Babka (SUSE) — SLUB maintainer</sub></td>
<td><code>security/keys</code></td>
<td><img src="https://img.shields.io/badge/Acked--by-8BC34A?style=flat-square" /></td>
<td><sub>04/06/2026</sub></td>
</tr>
<tr>
<td align="center"><code>2</code></td>
<td><a href="https://lore.kernel.org/all/20260607111933.6398-1-med08elkadiri@gmail.com/"><b>media: venus: Annotate flex arrays with __counted_by()</b></a><br><sub>Improve run-time bounds checking via CONFIG_UBSAN_BOUNDS and compile-time __builtin_dynamic_object_size().</sub><br><sub>Reviewed-by: Dmitry Baryshkov (Qualcomm)</sub></td>
<td><code>media/venus</code></td>
<td><img src="https://img.shields.io/badge/Reviewed--by-8BC34A?style=flat-square" /></td>
<td><sub>11/05/2026</sub></td>
</tr>
<tr>
<td align="center"><code>1</code></td>
<td><a href="https://lore.kernel.org/all/20260322150733.45817-1-med08elkadiri@gmail.com/"><b>sfc: fix spelling mistake</b></a><br><sub>Forwarded upstream by maintainer Edward Cree for inclusion in next firmware header regeneration.</sub></td>
<td><code>net/sfc</code></td>
<td><img src="https://img.shields.io/badge/Accepted-4CAF50?style=flat-square" /></td>
<td><sub>22/03/2026</sub></td>
</tr>
</table>

<br>

<div align="center">

<table>
<tr>
<td align="center"><strong>Total</strong><br><code>5</code></td>
<td align="center"><strong>Accepted</strong><br><code>1</code></td>
<td align="center"><strong>Reviewed / Acked</strong><br><code>2</code></td>
<td align="center"><strong>Subsystems</strong><br><code>mm · cred · keys · media · net</code></td>
</tr>
</table>

> 🟢 **Accepted / Reviewed / Acked** &nbsp; 🔵 **Submitted**

<sub>Last updated: 07/06/2026</sub>

</div>

<!-- KERNEL_PATCHES_END -->

---

### Technical Focus

| Area | Details |
|------|---------|
| Kernel / OS Internals | Linux kernel, macOS/XNU, syscall interfaces, VFS, memory management |
| Security Hardening | Slab isolation, SLUB allocator, cross-cache attack mitigation, fd safety |
| Concurrency | Lock-free structures, atomics, memory ordering, spinlocks, RCU |
| Performance | perf, flamegraphs, strace, eBPF, Google Benchmark |
| Cross-platform | Linux, macOS, FreeBSD, compile-time platform abstraction |

---

### Tools

<p align="center">
<img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/c-colored.svg" alt="C" title="C" width="32" height="32" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/cplusplus-colored.svg" alt="C++" title="C++" width="32" height="32" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/linux-colored.svg" alt="Linux" title="Linux" width="32" height="32" /> <img src="https://raw.githubusercontent.com/danielcranney/profileme-dev/main/public/icons/skills/macos-colored.svg" alt="macOS" title="macOS" width="32" height="32" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/gnubash-colored.svg" alt="Bash" title="Bash" width="32" height="32" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/git-colored.svg" alt="Git" title="Git" width="32" height="32" />
</p>

<p align="center">
<code>C</code> · <code>C++17</code> · <code>POSIX</code> · <code>x86_64/ARM64</code> · <code>CMake</code> · <code>Make/Kbuild</code> · <code>GDB/LLDB</code> · <code>perf</code> · <code>strace</code> · <code>eBPF</code> · <code>Git</code> · <code>Linux</code> · <code>macOS/XNU</code>
</p>

---

### Activity

<div align="center">

<img src="https://github-readme-streak-stats.herokuapp.com/?user=medelkadiri&theme=github-dark-blue&hide_border=true" width="60%" />

<img src="https://github-readme-activity-graph.vercel.app/graph?username=medelkadiri&theme=github-dark&hide_border=true&area=true" width="97%" />

</div>
