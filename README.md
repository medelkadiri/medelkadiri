<div align="center">

# Mohammed EL Kadiri

**Systems Software Engineer · Linux Kernel Contributor · Security & Reliability Engineering**

Systems software engineer specializing in Linux kernel development, operating-system internals, security hardening, and low-level reliability engineering.  
Contributor to upstream Linux subsystems including media, credentials, keys, fscrypt, and networking; experienced in debugging kernel faults, improving parser correctness, and hardening memory-sensitive code in C/C++17.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohammedelkadiri/)
[![Medium](https://img.shields.io/badge/Medium-000000?style=flat&logo=medium&logoColor=white)](https://medium.com/@medelkadiri)
[![Linux Kernel](https://img.shields.io/badge/Linux_Kernel-Contributor-FCC624?style=flat&logo=linux&logoColor=black)](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com)

</div>

---

### What This GitHub Contains

This is my systems-engineering workspace: low-level software that operates at the boundary between hardware, kernels, and applications. The work here covers resource lifetime management, memory allocation, concurrency, process execution, IPC, observability, and kernel-level security and reliability fixes.

My approach emphasizes correctness under failure, explicit ownership, measurable performance, and maintainable interfaces for systems software.

---

### What I Build

<table>
<tr>
<td width="50%">

**[systems-engineering](https://github.com/medelkadiri/systems-engineering)**

Production-oriented C++17 systems components emphasizing correctness, secure resource ownership, concurrency safety, benchmarking, and cross-platform portability.

`RAII fd wrapper` · `lock-free stack` · `memory pool` · `thread pool` · `ring buffer`

![C++17](https://img.shields.io/badge/C++17-00599C?style=flat&logo=cplusplus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat&logo=apple&logoColor=white)

</td>
<td width="50%">

**[jakashell](https://github.com/medelkadiri/jakashell)**

Linux shell and process-management project exploring zero-copy IPC, CPU-affinity-aware execution, memory mapping, and eBPF-based runtime telemetry.

`mmap IPC` · `CPU affinity` · `eBPF tracing` · `process management`

![C](https://img.shields.io/badge/C-A8B9CC?style=flat&logo=c&logoColor=black)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![eBPF](https://img.shields.io/badge/eBPF-FF6600?style=flat)

</td>
</tr>
<tr>
<td colspan="2" align="center">

**[Linux Kernel Contributions](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com)**

Upstream Linux kernel work spanning media-driver correctness, flexible-array bounds hardening, key-management robustness, slab-cache isolation, and fscrypt/keyring reliability analysis.

![Kernel](https://img.shields.io/badge/Linux_Kernel-Contributor-FCC624?style=flat&logo=linux&logoColor=black)

</td>
</tr>
</table>

---

<!-- KERNEL_PATCHES_START -->

### Linux Kernel Contributions

<div align="center">

*Upstream contributions and credited kernel reports — tracked through [lore.kernel.org](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com), maintainer trees, and stable-kernel notifications*

</div>

<br>

<table>
<tr>
<th align="center">#</th>
<th>Contribution</th>
<th>Subsystem</th>
<th>Status</th>
<th>Date</th>
</tr>

<tr>
<td align="center"><code>10</code></td>
<td>
<b>fscrypt keyring / filesystem-reclaim lockdep issue</b>
<br>
<sub>Reported an fscrypt/keyring locking issue associated with filesystem reclaim and keyring locking. The resulting fscrypt redesign replaced the master-key user keyring with a simpler per-user linked-list model while retaining quota accounting.</sub>
<br>
<sub>Reported-by credit in upstream commit <code>696c030e1e34</code> · Resolution authored by Eric Biggers · Added to the 6.12-stable and 7.1-stable trees.</sub>
</td>
<td><code>fs/crypto · security/keys</code></td>
<td><img src="https://img.shields.io/badge/Credited_in_Upstream_Fix-4CAF50?style=flat-square" /></td>
<td><sub>14/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>9</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22KEYS%3A+avoid+filesystem+reclaim+while+holding+keyring-%3Esem%22"><b>KEYS: avoid filesystem reclaim while holding keyring-&gt;sem</b></a>
<br>
<sub>Proposed a targeted memalloc_nofs_save()/restore() mitigation for a keyring-&gt;sem → filesystem-reclaim → keyring-&gt;sem lockdep cycle reported by syzbot.</sub>
<br>
<sub>The investigation contributed to the subsequent upstream fscrypt redesign credited above.</sub>
</td>
<td><code>security/keys</code></td>
<td><img src="https://img.shields.io/badge/Submitted-2196F3?style=flat-square" /></td>
<td><sub>14/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>8</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22keys%3A+keyctl_pkey%3A+replace+BUG+with+return+-EOPNOTSUPP%22"><b>keys: keyctl_pkey: replace BUG with return -EOPNOTSUPP</b></a>
<br>
<sub>Replace BUG() paths in asymmetric-key operation dispatch with -EOPNOTSUPP, preserving kernel availability and providing explicit unsupported-operation handling.</sub>
<br>
<sub>Reviewed-by: Jarkko Sakkinen · Queued in <a href="https://git.kernel.org/pub/scm/linux/kernel/git/jarkko/linux-tpmdd.git/log/?h=for-next-keys">for-next-keys</a></sub>
</td>
<td><code>security/keys</code></td>
<td><img src="https://img.shields.io/badge/Queued-for--next--keys-4CAF50?style=flat-square" /></td>
<td><sub>13/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>7</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22keys%3A+request_key%3A+replace+BUG+with+return+-EINVAL%22"><b>keys: request_key: replace BUG with return -EINVAL</b></a>
<br>
<sub>Replace a BUG() path in request-key destination handling with -EINVAL, converting an invalid state into controlled error handling.</sub>
<br>
<sub>Reviewed-by: Jarkko Sakkinen · Queued in <a href="https://git.kernel.org/pub/scm/linux/kernel/git/jarkko/linux-tpmdd.git/log/?h=for-next-keys">for-next-keys</a></sub>
</td>
<td><code>security/keys</code></td>
<td><img src="https://img.shields.io/badge/Queued-for--next--keys-4CAF50?style=flat-square" /></td>
<td><sub>13/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>6</code></td>
<td>
<a href="https://lore.kernel.org/all/20260610125655.14523-3-med08elkadiri@gmail.com/"><b>media: venus: fix payload size calculation in parse_raw_formats()</b></a>
<br>
<sub>Corrected firmware-response parsing by accumulating each format entry's actual payload size rather than applying the final entry's plane count to all entries.</sub>
<br>
<sub>Reviewed-by: Dmitry Baryshkov, Qualcomm · Committed to <code>media.git/next</code></sub>
</td>
<td><code>media/venus</code></td>
<td><img src="https://img.shields.io/badge/Committed_to_media.git%2Fnext-4CAF50?style=flat-square" /></td>
<td><sub>10/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>5</code></td>
<td>
<a href="https://lore.kernel.org/all/20260610125655.14523-2-med08elkadiri@gmail.com/"><b>media: venus: fix payload size returned by parse_caps() and parse_alloc_mode()</b></a>
<br>
<sub>Fixed consumed-size accounting for variable-length HFI capability and allocation-mode responses, preventing parser desynchronization when advancing through firmware buffers.</sub>
<br>
<sub>Fixes: <code>9edaaa8e3e15</code> · Cc: stable@vger.kernel.org · Reviewed-by: Dmitry Baryshkov, Qualcomm · Committed to <code>media.git/next</code></sub>
</td>
<td><code>media/venus</code></td>
<td><img src="https://img.shields.io/badge/Committed_to_media.git%2Fnext-4CAF50?style=flat-square" /></td>
<td><sub>10/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>4</code></td>
<td>
<a href="https://lore.kernel.org/all/20260611070100.15012-1-med08elkadiri@gmail.com/"><b>cred: prevent slab cache merging for cred_jar</b></a>
<br>
<sub>Add SLAB_NO_MERGE to isolate credential objects from unrelated slab caches, reducing cross-cache attack surface and strengthening credential-memory integrity.</sub>
<br>
<sub>Reviewed-by: Kees Cook</sub>
</td>
<td><code>kernel/cred</code></td>
<td><img src="https://img.shields.io/badge/Reviewed--by-8BC34A?style=flat-square" /></td>
<td><sub>11/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>3</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22keys%3A+prevent+slab+cache+merging+for+key_jar%22"><b>keys: prevent slab cache merging for key_jar</b></a>
<br>
<sub>Add SLAB_NO_MERGE to isolate struct key allocations from unrelated caches as a defense-in-depth hardening measure.</sub>
<br>
<sub>Acked-by: Vlastimil Babka, SUSE · Queued in <a href="https://git.kernel.org/pub/scm/linux/kernel/git/jarkko/linux-tpmdd.git/log/?h=for-next-keys">for-next-keys</a></sub>
</td>
<td><code>security/keys</code></td>
<td><img src="https://img.shields.io/badge/Queued-for--next--keys-4CAF50?style=flat-square" /></td>
<td><sub>04/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>2</code></td>
<td>
<a href="https://lore.kernel.org/all/20260607111933.6398-1-med08elkadiri@gmail.com/"><b>media: venus: Annotate flex arrays with __counted_by()</b></a>
<br>
<sub>Annotated HFI flexible-array members with __counted_by() to improve CONFIG_UBSAN_BOUNDS coverage and enable stronger compiler object-size reasoning.</sub>
<br>
<sub>Reviewed-by: Dmitry Baryshkov, Qualcomm · Reviewed-by: Konrad Dybcio, Qualcomm · Committed to <code>media.git/next</code></sub>
</td>
<td><code>media/venus</code></td>
<td><img src="https://img.shields.io/badge/Committed_to_media.git%2Fnext-4CAF50?style=flat-square" /></td>
<td><sub>07/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>1</code></td>
<td>
<a href="https://lore.kernel.org/all/20260322150733.45817-1-med08elkadiri@gmail.com/"><b>sfc: fix spelling mistake</b></a>
<br>
<sub>Forwarded upstream by maintainer Edward Cree for inclusion during the next firmware-header regeneration.</sub>
</td>
<td><code>net/sfc</code></td>
<td><img src="https://img.shields.io/badge/Accepted-4CAF50?style=flat-square" /></td>
<td><sub>22/03/2026</sub></td>
</tr>

</table>

<br>

<div align="center">

<table>
<tr>
<td align="center"><strong>Patch Submissions</strong><br><code>9</code></td>
<td align="center"><strong>Committed / Queued / Accepted</strong><br><code>7</code></td>
<td align="center"><strong>Reviewed / Acked</strong><br><code>5</code></td>
<td align="center"><strong>Credited Upstream Report</strong><br><code>1</code></td>
<td align="center"><strong>Subsystems</strong><br><code>cred · keys · fscrypt · media · net</code></td>
</tr>
</table>

> 🟢 **Committed / Queued / Accepted** &nbsp; 🟩 **Reviewed / Acked** &nbsp; 🔵 **Submitted** &nbsp; 🟣 **Credited Report**

<sub>Last updated: 03/08/2026</sub>

</div>

<!-- KERNEL_PATCHES_END -->

---

### Technical Focus

| Area | Details |
|------|---------|
| Kernel / OS Internals | Linux kernel internals, syscall interfaces, VFS, keyrings, credentials, memory management, driver parsing |
| Security Hardening | Slab-cache isolation, cross-cache attack mitigation, bounds checking, flexible-array safety, controlled error handling |
| Reliability Engineering | Root-cause analysis, parser correctness, memory lifetime, fault handling, lockdep and syzbot-driven debugging |
| Concurrency | Lock-free structures, atomics, memory ordering, spinlocks, RCU, lock hierarchy analysis |
| Performance | perf, flamegraphs, strace, eBPF, Google Benchmark, CPU-affinity-aware execution |
| Cross-platform | Linux, macOS, FreeBSD, POSIX interfaces, compile-time platform abstraction |

---

### Tools

<p align="center">
<img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/c-colored.svg" alt="C" title="C" width="32" height="32" />
<img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/cplusplus-colored.svg" alt="C++" title="C++" width="32" height="32" />
<img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/linux-colored.svg" alt="Linux" title="Linux" width="32" height="32" />
<img src="https://raw.githubusercontent.com/danielcranney/profileme-dev/main/public/icons/skills/macos-colored.svg" alt="macOS" title="macOS" width="32" height="32" />
<img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/gnubash-colored.svg" alt="Bash" title="Bash" width="32" height="32" />
<img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/git-colored.svg" alt="Git" title="Git" width="32" height="32" />
</p>

<p align="center">
<code>C</code> · <code>C++17</code> · <code>POSIX</code> · <code>x86_64/ARM64</code> · <code>CMake</code> · <code>Make/Kbuild</code> · <code>GDB/LLDB</code> · <code>perf</code> · <code>strace</code> · <code>eBPF</code> · <code>Git</code> · <code>Linux</code> · <code>macOS/XNU</code>
</p>

---

### Activity

<div align="center">

*Kernel contributions tracked on [lore.kernel.org](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com) · Projects on [GitHub](https://github.com/medelkadiri?tab=repositories)*

</div>
