<div align="center">

# Mohammed EL Kadiri

**Systems Software Engineer · Linux Kernel Contributor · Security & Reliability Engineering**

Systems software engineer focused on Linux kernel development, operating-system internals, security hardening, and low-level reliability engineering.  
I work on correctness, memory safety, synchronization, and failure handling across kernel subsystems, firmware-facing drivers, key management, filesystem encryption, and performance-sensitive systems components in C/C++17.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohammedelkadiri/)
[![Medium](https://img.shields.io/badge/Medium-000000?style=flat&logo=medium&logoColor=white)](https://medium.com/@medelkadiri)
[![Linux Kernel](https://img.shields.io/badge/Linux_Kernel-Contributor-FCC624?style=flat&logo=linux&logoColor=black)](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com)

</div>

---

### What This GitHub Contains

This is my systems-engineering workspace: software that operates close to operating-system infrastructure, hardware interfaces, and runtime-critical services.

The projects and kernel work here focus on software that must remain correct under stress and failure: memory ownership, file-descriptor lifetime, concurrent execution, process control, IPC, binary-parser correctness, kernel locking, and security boundaries. My approach emphasizes explicit invariants, defensive design, measurable performance, and maintainable low-level code.

---

### What I Build

<table>
<tr>
<td width="50%">

**[systems-engineering](https://github.com/medelkadiri/systems-engineering)**

Production-oriented C++17 systems components designed around explicit ownership, secure resource management, concurrency safety, benchmarking, and cross-platform portability.

`RAII fd wrapper` · `lock-free stack` · `memory pool` · `thread pool` · `ring buffer`

![C++17](https://img.shields.io/badge/C++17-00599C?style=flat&logo=cplusplus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat&logo=apple&logoColor=white)

</td>
<td width="50%">

**[jakashell](https://github.com/medelkadiri/jakashell)**

Linux shell and process-management project exploring zero-copy IPC, memory-mapped communication, CPU-affinity-aware execution, and eBPF-based runtime telemetry.

`mmap IPC` · `CPU affinity` · `eBPF tracing` · `process management`

![C](https://img.shields.io/badge/C-A8B9CC?style=flat&logo=c&logoColor=black)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![eBPF](https://img.shields.io/badge/eBPF-FF6600?style=flat)

</td>
</tr>
<tr>
<td colspan="2" align="center">

**[Linux Kernel Contributions](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com)**

Upstream Linux kernel work across driver correctness, memory-safety hardening, key-management reliability, allocator isolation, and filesystem-encryption debugging.

![Kernel](https://img.shields.io/badge/Linux_Kernel-Contributor-FCC624?style=flat&logo=linux&logoColor=black)

</td>
</tr>
</table>

---

<!-- KERNEL_PATCHES_START -->

### Linux Kernel Contributions

<div align="center">

*Upstream Linux kernel patches and credited reports — tracked through [lore.kernel.org](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com), subsystem maintainer trees, and stable-kernel notifications*

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
<sub>Investigated and reported a locking issue in fscrypt master-key user tracking. The issue involved an interaction between keyring locking and filesystem memory reclaim that could produce a lockdep warning under automated kernel fuzzing. The upstream resolution simplified fscrypt's user-claim tracking by replacing an internal keyring with an explicit linked-list representation while retaining per-user quota accounting.</sub>
<br>
<sub>This work crosses filesystem encryption, kernel key management, memory reclaim, lock ordering, and syzbot-guided debugging.</sub>
<br>
<sub>Reported-by credit in upstream commit <code>696c030e1e34</code> · Fix authored by Eric Biggers · Backported to the 6.12-stable and 7.1-stable kernel trees.</sub>
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
<sub>Proposed a targeted mitigation for a lock-ordering cycle between the kernel keyring semaphore and filesystem memory reclaim. The patch uses <code>memalloc_nofs_save()</code> and <code>memalloc_nofs_restore()</code> to prevent filesystem reclaim while updating a keyring associative array, avoiding the allocation path that can re-enter the same locking domain.</sub>
<br>
<sub>Demonstrates analysis of difficult-to-reproduce kernel concurrency failures using lockdep traces, syzbot reports, lock hierarchy reasoning, and allocation-context constraints.</sub>
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
<sub>Replaced fatal <code>BUG()</code> assertions in asymmetric-key operation dispatch with the standard <code>-EOPNOTSUPP</code> error. Unsupported operation types are now reported safely to userspace instead of causing a system-wide kernel crash.</sub>
<br>
<sub>This improves availability and API resilience in a security-sensitive subsystem by converting an unexpected state into explicit, recoverable error handling.</sub>
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
<sub>Replaced a <code>BUG()</code> path in request-key destination handling with <code>-EINVAL</code>. Invalid or unimplemented keyring destination states now follow the kernel's normal error-return model rather than triggering a fatal assertion.</sub>
<br>
<sub>This is a reliability and hardening improvement at the userspace/kernel boundary: invalid input or unsupported state is rejected safely without compromising the availability of the running system.</sub>
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
<sub>Fixed binary parsing of firmware responses in Qualcomm's Venus video-codec driver. The previous implementation calculated the total payload size using the plane count from only the final format record. If records contained different plane counts, the parser could advance through the firmware buffer incorrectly. The fix accumulates each record's actual size while parsing.</sub>
<br>
<sub>This preserves a critical driver/firmware protocol invariant: parser state must advance by the exact number of bytes consumed, preventing malformed capability data and incorrect buffer traversal.</sub>
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
<sub>Corrected consumed-byte accounting in two variable-length firmware-message parsers in the Qualcomm Venus driver. The functions returned only fixed-header sizes and omitted the flexible-array payload. Since the higher-level parser uses those values to find the next message in the firmware response buffer, underreporting could desynchronize parsing when messages are packed together.</sub>
<br>
<sub>The fix ensures each parser reports its complete consumed size: header plus variable-length entries. This is essential for reliable device-driver protocol handling and robust parsing of externally supplied binary data.</sub>
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
<sub>Added <code>SLAB_NO_MERGE</code> to the allocator cache used for Linux credential objects (<code>struct cred</code>). Credential objects contain process identity and authorization state, including user and group IDs, capabilities, and security-relevant execution context. The change keeps these objects in a dedicated slab cache instead of allowing allocation-cache sharing with unrelated object types.</sub>
<br>
<sub>This is defense-in-depth hardening against cross-cache heap-corruption techniques, reducing the risk that an unrelated memory-safety bug can be leveraged to corrupt security-critical credential data.</sub>
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
<sub>Added <code>SLAB_NO_MERGE</code> to the slab cache used for <code>struct key</code>, a core object in Linux key management. The change prevents key objects from sharing a compatible allocator cache with unrelated kernel object types.</sub>
<br>
<sub>Dedicated allocation domains strengthen isolation in a subsystem responsible for credentials, secrets, certificates, and cryptographic key material, making cross-cache heap-corruption exploitation more difficult.</sub>
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
<sub>Annotated flexible-array members in Qualcomm Venus HFI protocol structures with <code>__counted_by()</code>. These annotations explicitly associate each variable-length array with the field that stores its element count, allowing compilers and kernel sanitizers to determine the valid bounds of allocated objects more accurately.</sub>
<br>
<sub>This is proactive memory-safety hardening for a driver that processes firmware-provided data. It improves run-time bounds checking through <code>CONFIG_UBSAN_BOUNDS</code> and strengthens compiler object-size analysis.</sub>
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
<sub>Submitted a documentation and source-comment correction for the Solarflare network-driver firmware interface. The change followed the complete upstream Linux kernel process: identifying an issue, preparing a standards-compliant patch, responding through the maintainer workflow, and having the change forwarded for a future generated firmware-header update.</sub>
<br>
<sub>Demonstrates practical familiarity with upstream kernel contribution norms, subsystem ownership, maintainer review, and integration workflows.</sub>
<br>
<sub>Forwarded upstream by maintainer Edward Cree for inclusion in the next firmware-header regeneration.</sub>
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
<td align="center">
<strong>Upstream Patches Submitted</strong><br>
<code>9</code><br>
<sub>Kernel patches and patch series sent to maintainers</sub>
</td>
<td align="center">
<strong>Accepted, Queued, or Committed</strong><br>
<code>7</code><br>
<sub>Work that progressed into maintainer trees or an upstream integration path</sub>
</td>
<td align="center">
<strong>Maintainer-Validated Patches</strong><br>
<code>7</code><br>
<sub>Patches receiving formal Reviewed-by or Acked-by tags from kernel maintainers</sub>
</td>
<td align="center">
<strong>Stable-Kernel Impact</strong><br>
<code>1</code><br>
<sub>Upstream fscrypt issue report credited in a fix backported to stable kernels</sub>
</td>
</tr>
</table>

> **What these numbers mean:** upstream patch submission demonstrates contribution velocity; accepted, queued, and committed work demonstrates maintainer confidence and integration progress; formal review demonstrates technical validation by subsystem experts; stable-kernel impact demonstrates relevance beyond mainline development.

<sub>Last updated: 03/08/2026</sub>

</div>

<!-- KERNEL_PATCHES_END -->

---

### Technical Focus

| Area | Details |
|------|---------|
| Kernel / OS Internals | Linux kernel internals, syscall interfaces, VFS, keyrings, credentials, filesystem encryption, memory management, driver parsing |
| Security Hardening | Slab-cache isolation, cross-cache attack mitigation, bounds checking, flexible-array safety, secure error handling |
| Reliability Engineering | Root-cause analysis, parser invariants, memory lifetime, fault handling, lockdep analysis, syzbot-driven debugging |
| Concurrency | Lock-free structures, atomics, memory ordering, spinlocks, RCU, lock hierarchy and deadlock analysis |
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
