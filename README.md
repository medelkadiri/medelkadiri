<div align="center">

# Mohammed EL Kadiri

**Senior Systems Software Engineer · Linux Kernel Contributor · Security & Reliability Engineering**

Systems software engineer focused on Linux kernel development, operating-system internals, security hardening, and low-level reliability engineering.  
I work on issues where correctness, memory safety, synchronization, and failure handling matter: kernel subsystems, firmware-facing drivers, key management, filesystem encryption, and performance-critical systems components in C/C++17.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohammedelkadiri/)
[![Medium](https://img.shields.io/badge/Medium-000000?style=flat&logo=medium&logoColor=white)](https://medium.com/@medelkadiri)
[![Linux Kernel](https://img.shields.io/badge/Linux_Kernel-Contributor-FCC624?style=flat&logo=linux&logoColor=black)](https://lore.kernel.org/all/?q=med08elkadiri%40gmail.com)

</div>

---

### What This GitHub Contains

This is my systems-engineering workspace: software that operates close to the operating system, hardware interfaces, and runtime infrastructure.

The projects and kernel work here focus on the parts of a system that must remain correct under stress and failure: memory ownership, file-descriptor lifetime, concurrent execution, process control, IPC, parser correctness, kernel locking, and security boundaries. My engineering approach prioritizes clear invariants, measurable behavior, defensive design, and maintainable low-level code.

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

Upstream Linux kernel contributions spanning driver correctness, memory-safety hardening, key-management reliability, slab-cache isolation, and filesystem-encryption debugging.

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
<sub>Investigated and reported a kernel locking problem affecting fscrypt master-key user tracking. The issue involved the interaction between keyring locking and filesystem memory reclaim, which could trigger a lockdep warning under fuzzing. The upstream fix simplified fscrypt's user-claim tracking model by replacing an internal keyring with an explicit linked list while preserving per-user key-quota accounting.</sub>
<br>
<sub>Recruiter context: systems-level debugging across filesystem encryption, key management, locking, memory reclaim, and automated kernel fuzzing.</sub>
<br>
<sub>Reported-by credit in upstream commit <code>696c030e1e34</code> · Fix authored by Eric Biggers · Added to the 6.12-stable and 7.1-stable trees.</sub>
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
<sub>Proposed a focused mitigation for a lock-ordering cycle involving the kernel keyring semaphore and filesystem memory reclaim. The patch uses the kernel's <code>memalloc_nofs_save()</code>/<code>memalloc_nofs_restore()</code> mechanism to prevent filesystem reclaim while modifying a keyring associative array, removing the conditions that can lead to recursive locking.</sub>
<br>
<sub>Recruiter context: demonstrates root-cause analysis of concurrency bugs that are difficult to reproduce, using lockdep and syzbot reports to reason about kernel lock hierarchy and memory-allocation behavior.</sub>
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
<sub>Replaced fatal <code>BUG()</code> assertions in asymmetric-key operation handling with a standard <code>-EOPNOTSUPP</code> error return. Instead of terminating the kernel when an unsupported operation reaches an unexpected dispatch path, the kernel now fails safely and communicates the unsupported condition to userspace.</sub>
<br>
<sub>Recruiter context: converts a potential system-wide crash into controlled fault handling, improving availability and making the API behavior safer for malformed, unexpected, or future operation types.</sub>
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
<sub>Replaced a <code>BUG()</code> path in request-key destination handling with <code>-EINVAL</code>. Invalid or unimplemented keyring destination states are now rejected through normal error handling rather than triggering a kernel crash.</sub>
<br>
<sub>Recruiter context: a small but high-value reliability change in a security-sensitive kernel subsystem. It strengthens the kernel's handling of invalid states and reduces crash exposure at the userspace/kernel boundary.</sub>
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
<sub>Fixed incorrect parsing of firmware responses in Qualcomm's Venus video-codec driver. The original code calculated the size of all raw-format records using the plane count from only the final record. When records had different numbers of planes, the parser could advance by the wrong number of bytes. The fix accumulates the actual size of each individual record during parsing.</sub>
<br>
<sub>Recruiter context: correctness work at a hardware/firmware boundary, where inaccurate binary-buffer parsing can desynchronize protocol handling and lead to invalid reads, corrupted capability data, or device instability.</sub>
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
<sub>Corrected consumed-byte accounting in two variable-length firmware-message parsers in the Qualcomm Venus driver. Both functions previously returned only the fixed header size while omitting their flexible-array payload. Because the higher-level parser uses that return value to locate the next message, this could cause parser desynchronization when multiple responses were present in the same buffer.</sub>
<br>
<sub>Recruiter context: identifies and fixes a subtle protocol-parser invariant: every parser must report exactly how much input it consumed. This is essential for robust device-driver communication and memory-safe binary parsing.</sub>
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
<sub>Added <code>SLAB_NO_MERGE</code> to the allocator cache used for Linux credential objects (<code>struct cred</code>). Credentials represent process identity and authorization state, including user and group IDs, capabilities, and security-relevant execution context. Preventing this cache from merging with unrelated allocation types improves object isolation.</sub>
<br>
<sub>Recruiter context: defense-in-depth kernel hardening against cross-cache memory-corruption techniques, reducing the opportunity for an unrelated heap bug to be used to corrupt security-critical credential data.</sub>
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
<sub>Added <code>SLAB_NO_MERGE</code> to the slab cache used for <code>struct key</code>, a core object in Linux key management. The change ensures key objects are allocated from a dedicated cache rather than sharing an allocator cache with unrelated objects of compatible size.</sub>
<br>
<sub>Recruiter context: security hardening at the kernel allocator layer. Dedicated allocation domains make exploitation of cross-cache heap-corruption bugs more difficult in a subsystem responsible for credentials, secrets, certificates, and cryptographic keys.</sub>
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
<sub>Annotated flexible-array members in Qualcomm Venus HFI protocol structures with <code>__counted_by()</code>. The annotations explicitly connect each variable-length array to its element-count field, allowing the compiler and kernel sanitizers to reason more accurately about the valid bounds of the allocated object.</sub>
<br>
<sub>Recruiter context: proactive memory-safety hardening in a driver that processes firmware-provided data. The change improves run-time out-of-bounds detection through <code>CONFIG_UBSAN_BOUNDS</code> and strengthens compile-time object-size analysis.</sub>
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
<sub>Submitted a documentation and source-comment correction for the Solarflare network-driver firmware interface. While small, this contribution followed the full upstream Linux kernel contribution process: identifying the issue, preparing a standards-compliant patch, engaging with the subsystem maintainer, and having the change forwarded for inclusion in a future generated firmware header update.</sub>
<br>
<sub>Recruiter context: demonstrates familiarity with the Linux kernel development workflow, including patch submission, maintainer review, and subsystem integration.</sub>
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
<strong>Linux Kernel Patches Submitted</strong><br>
<code>9</code><br>
<sub>Patch series and individual patches sent upstream</sub>
</td>
<td align="center">
<strong>Patches Progressed Upstream</strong><br>
<code>7</code><br>
<sub>Committed, queued by maintainers, or accepted for integration</sub>
</td>
<td align="center">
<strong>Maintainer Reviews / Acks</strong><br>
<code>6</code><br>
<sub>Patches receiving formal review or acknowledgement from subsystem maintainers</sub>
</td>
<td align="center">
<strong>Upstream Bug Report Credit</strong><br>
<code>1</code><br>
<sub>Reported fscrypt issue credited in an upstream fix backported to stable kernels</sub>
</td>
<td align="center">
<strong>Kernel Areas</strong><br>
<code>5</code><br>
<sub>cred · keys · fscrypt · media · net</sub>
</td>
</tr>
</table>

> 🟢 **Progressed Upstream** = committed, queued, or accepted &nbsp; 🟩 **Reviewed / Acked** = maintainer validation received &nbsp; 🔵 **Submitted** = sent upstream and under review &nbsp; 🟣 **Upstream Credit** = issue report credited in a merged kernel fix

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
