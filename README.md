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
<th align="center" width="5%">#</th>
<th>Contribution</th>
<th align="center" width="16%">Subsystem</th>
<th align="center" width="13%">Status</th>
<th align="center" width="10%">Date</th>
</tr>

<tr>
<td align="center"><code>10</code></td>
<td>
<b>fscrypt keyring / filesystem-reclaim lockdep issue</b>
<br>
<sub>Investigated and reported a locking issue in fscrypt master-key user tracking. The issue involved an interaction between keyring locking and filesystem memory reclaim that could produce a lockdep warning under automated kernel fuzzing. The upstream resolution simplified fscrypt's user-claim tracking by replacing an internal keyring with an explicit linked-list representation while retaining per-user quota accounting.</sub>
<br>
<sub>Reported-by credit in upstream commit <code>696c030e1e34</code> · Fix authored by Eric Biggers · Added to the 6.12-stable and 7.1-stable trees.</sub>
</td>
<td align="center"><code>fs/crypto</code><br><code>security/keys</code></td>
<td align="center"><code>Credited fix</code></td>
<td align="center"><sub>14/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>9</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22KEYS%3A+avoid+filesystem+reclaim+while+holding+keyring-%3Esem%22"><b>KEYS: avoid filesystem reclaim while holding keyring-&gt;sem</b></a>
<br>
<sub>Proposed a targeted mitigation for a lock-ordering cycle between the kernel keyring semaphore and filesystem memory reclaim. The patch uses <code>memalloc_nofs_save()</code> and <code>memalloc_nofs_restore()</code> to prevent filesystem reclaim while updating a keyring associative array, avoiding an allocation path that can re-enter the same locking domain.</sub>
<br>
<sub>The investigation contributed to the subsequent upstream fscrypt redesign credited above.</sub>
</td>
<td align="center"><code>security/keys</code></td>
<td align="center"><code>Submitted</code></td>
<td align="center"><sub>14/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>8</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22keys%3A+keyctl_pkey%3A+replace+BUG+with+return+-EOPNOTSUPP%22"><b>keys: keyctl_pkey: replace BUG with return -EOPNOTSUPP</b></a>
<br>
<sub>Replaced fatal <code>BUG()</code> assertions in asymmetric-key operation dispatch with the standard <code>-EOPNOTSUPP</code> error. Unsupported operation types are now returned safely to userspace instead of causing a system-wide kernel crash.</sub>
<br>
<sub>This aligns the code path with normal kernel error-handling conventions and preserves system availability for unsupported requests.</sub>
<br>
<sub>Reviewed-by: Jarkko Sakkinen · Queued in <a href="https://git.kernel.org/pub/scm/linux/kernel/git/jarkko/linux-tpmdd.git/log/?h=for-next-keys">for-next-keys</a></sub>
</td>
<td align="center"><code>security/keys</code></td>
<td align="center"><code>Queued</code></td>
<td align="center"><sub>13/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>7</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22keys%3A+request_key%3A+replace+BUG+with+return+-EINVAL%22"><b>keys: request_key: replace BUG with return -EINVAL</b></a>
<br>
<sub>Replaced a <code>BUG()</code> path in request-key destination handling with <code>-EINVAL</code>. Invalid or unimplemented keyring destination states now follow the kernel's standard error-return model rather than triggering a fatal assertion.</sub>
<br>
<sub>This hardens a userspace-facing path in the key-management subsystem by treating invalid state as a recoverable error.</sub>
<br>
<sub>Reviewed-by: Jarkko Sakkinen · Queued in <a href="https://git.kernel.org/pub/scm/linux/kernel/git/jarkko/linux-tpmdd.git/log/?h=for-next-keys">for-next-keys</a></sub>
</td>
<td align="center"><code>security/keys</code></td>
<td align="center"><code>Queued</code></td>
<td align="center"><sub>13/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>6</code></td>
<td>
<a href="https://lore.kernel.org/all/20260610125655.14523-3-med08elkadiri@gmail.com/"><b>media: venus: fix payload size calculation in parse_raw_formats()</b></a>
<br>
<sub>Fixed binary parsing of firmware responses in Qualcomm's Venus video-codec driver. The previous implementation calculated the total payload size using the plane count from only the final format record. If records contained different plane counts, the parser could advance through the firmware buffer incorrectly. The fix accumulates each record's actual size while parsing.</sub>
<br>
<sub>This preserves the protocol invariant that parser state advances by the exact number of bytes consumed.</sub>
<br>
<sub>Reviewed-by: Dmitry Baryshkov, Qualcomm · Committed to <code>media.git/next</code></sub>
</td>
<td align="center"><code>media/venus</code></td>
<td align="center"><code>Committed</code></td>
<td align="center"><sub>10/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>5</code></td>
<td>
<a href="https://lore.kernel.org/all/20260610125655.14523-2-med08elkadiri@gmail.com/"><b>media: venus: fix payload size returned by parse_caps() and parse_alloc_mode()</b></a>
<br>
<sub>Corrected consumed-byte accounting in two variable-length firmware-message parsers in the Qualcomm Venus driver. The functions returned only fixed-header sizes and omitted the flexible-array payload. Since the higher-level parser uses those values to locate the next message in a firmware response buffer, underreporting could desynchronize parsing when messages are packed together.</sub>
<br>
<sub>The fix returns the full consumed size for each message: fixed header plus variable-length entries.</sub>
<br>
<sub>Fixes: <code>9edaaa8e3e15</code> · Cc: stable@vger.kernel.org · Reviewed-by: Dmitry Baryshkov, Qualcomm · Committed to <code>media.git/next</code></sub>
</td>
<td align="center"><code>media/venus</code></td>
<td align="center"><code>Committed</code></td>
<td align="center"><sub>10/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>4</code></td>
<td>
<a href="https://lore.kernel.org/all/20260611070100.15012-1-med08elkadiri@gmail.com/"><b>cred: prevent slab cache merging for cred_jar</b></a>
<br>
<sub>Added <code>SLAB_NO_MERGE</code> to the allocator cache used for Linux credential objects (<code>struct cred</code>). Credential objects contain process identity and authorization state, including user and group IDs, capabilities, and security-relevant execution context. The change keeps these objects in a dedicated slab cache instead of allowing allocation-cache sharing with unrelated object types.</sub>
<br>
<sub>This improves isolation for one of the kernel's most security-sensitive object types.</sub>
<br>
<sub>Reviewed-by: Kees Cook</sub>
</td>
<td align="center"><code>kernel/cred</code></td>
<td align="center"><code>Reviewed</code></td>
<td align="center"><sub>11/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>3</code></td>
<td>
<a href="https://lore.kernel.org/all/?q=s%3A%22keys%3A+prevent+slab+cache+merging+for+key_jar%22"><b>keys: prevent slab cache merging for key_jar</b></a>
<br>
<sub>Added <code>SLAB_NO_MERGE</code> to the slab cache used for <code>struct key</code>, a core object in Linux key management. The change prevents key objects from sharing a compatible allocator cache with unrelated kernel object types.</sub>
<br>
<sub>Dedicated allocation domains strengthen isolation in a subsystem responsible for credentials, secrets, certificates, and cryptographic key material.</sub>
<br>
<sub>Acked-by: Vlastimil Babka, SUSE · Queued in <a href="https://git.kernel.org/pub/scm/linux/kernel/git/jarkko/linux-tpmdd.git/log/?h=for-next-keys">for-next-keys</a></sub>
</td>
<td align="center"><code>security/keys</code></td>
<td align="center"><code>Queued</code></td>
<td align="center"><sub>04/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>2</code></td>
<td>
<a href="https://lore.kernel.org/all/20260607111933.6398-1-med08elkadiri@gmail.com/"><b>media: venus: Annotate flex arrays with __counted_by()</b></a>
<br>
<sub>Annotated flexible-array members in Qualcomm Venus HFI protocol structures with <code>__counted_by()</code>. The annotations associate each variable-length array with its element-count field, allowing compilers and kernel sanitizers to determine the valid bounds of allocated objects more accurately.</sub>
<br>
<sub>This improves run-time bounds checking through <code>CONFIG_UBSAN_BOUNDS</code> and strengthens compiler object-size analysis for firmware-facing data structures.</sub>
<br>
<sub>Reviewed-by: Dmitry Baryshkov, Qualcomm · Reviewed-by: Konrad Dybcio, Qualcomm · Committed to <code>media.git/next</code></sub>
</td>
<td align="center"><code>media/venus</code></td>
<td align="center"><code>Committed</code></td>
<td align="center"><sub>07/06/2026</sub></td>
</tr>

<tr>
<td align="center"><code>1</code></td>
<td>
<a href="https://lore.kernel.org/all/20260322150733.45817-1-med08elkadiri@gmail.com/"><b>sfc: fix spelling mistake</b></a>
<br>
<sub>Submitted a documentation and source-comment correction for the Solarflare network-driver firmware interface. The change followed the upstream Linux kernel workflow: patch submission, subsystem maintainer review, and forwarding for inclusion during a future generated firmware-header update.</sub>
<br>
<sub>Forwarded upstream by maintainer Edward Cree.</sub>
</td>
<td align="center"><code>net/sfc</code></td>
<td align="center"><code>Accepted</code></td>
<td align="center"><sub>22/03/2026</sub></td>
</tr>

</table>

<br>

<div align="center">

<table>
<tr>
<td align="center">
<strong>Upstream Submissions</strong><br>
<code>9</code><br>
<sub>Patch series and individual patches posted to kernel lists</sub>
</td>
<td align="center">
<strong>Integration Progress</strong><br>
<code>7</code><br>
<sub>Accepted, queued in maintainer trees, or committed</sub>
</td>
<td align="center">
<strong>Maintainer Review</strong><br>
<code>7</code><br>
<sub>Contributions carrying Reviewed-by or Acked-by tags</sub>
</td>
<td align="center">
<strong>Stable Tree Credit</strong><br>
<code>1</code><br>
<sub>Reported issue referenced by a stable-kernel fix</sub>
</td>
</tr>
</table>

<sub>Statuses reflect different stages of upstream development; a patch may be both reviewed and queued or committed.</sub><br>
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
