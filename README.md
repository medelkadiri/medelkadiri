<!-- KERNEL_PATCHES_START -->

### Linux Kernel Patches

<div align="center">

*Upstream contributions to the Linux kernel - tracked from [lore.kernel.org](https://lore.kernel.org/all/?q=from%3Amed08elkadiri%40gmail.com)*

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
<td align="center"><code>4</code></td>
<td><a href="https://lore.kernel.org/all/20260606142558.13809-1-med08elkadiri@gmail.com/"><b>cred: prevent slab cache merging for cred_jar</b></a><br><sub>Add SLAB_NO_MERGE to isolate struct cred (uid, gid, capabilities) from cross-cache heap attacks.</sub></td>
<td><code>kernel/cred</code></td>
<td><img src="https://img.shields.io/badge/Submitted-2196F3?style=flat-square" /></td>
<td><sub>06/06/2026</sub></td>
</tr>
<tr>
<td align="center"><code>3</code></td>
<td><a href="https://lore.kernel.org/all/20260604125034.13757-1-med08elkadiri@gmail.com/"><b>keys: prevent slab cache merging for key_jar</b></a><br><sub>Add SLAB_NO_MERGE to isolate struct key from cross-cache heap attacks.</sub><br><sub>Reviewed-by: Jarkko Sakkinen · Acked-by: Vlastimil Babka (SUSE)</sub></td>
<td><code>security/keys</code></td>
<td><img src="https://img.shields.io/badge/Applied-4CAF50?style=flat-square" /></td>
<td><sub>04/06/2026</sub></td>
</tr>
<tr>
<td align="center"><code>2</code></td>
<td><a href="https://lore.kernel.org/all/20260607111933.6398-1-med08elkadiri@gmail.com/"><b>media: venus: Annotate flex arrays with __counted_by()</b></a><br><sub>Improve run-time bounds checking via CONFIG_UBSAN_BOUNDS and compile-time __builtin_dynamic_object_size().</sub><br><sub>Reviewed-by: Dmitry Baryshkov (Qualcomm) · Reviewed-by: Konrad Dybcio (Qualcomm)</sub></td>
<td><code>media/venus</code></td>
<td><img src="https://img.shields.io/badge/Reviewed--by-8BC34A?style=flat-square" /></td>
<td><sub>07/06/2026</sub></td>
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
<td align="center"><strong>Total</strong><br><code>4</code></td>
<td align="center"><strong>Applied / Accepted</strong><br><code>2</code></td>
<td align="center"><strong>Reviewed / Acked</strong><br><code>2</code></td>
<td align="center"><strong>Subsystems</strong><br><code>cred · keys · media · net</code></td>
</tr>
</table>

> 🟢 **Applied / Accepted / Reviewed / Acked** &nbsp; 🔵 **Submitted**

<sub>Last updated: 08/06/2026</sub>

</div>

<!-- KERNEL_PATCHES_END -->
