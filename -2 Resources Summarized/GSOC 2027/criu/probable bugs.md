hought for 4s, 665 tokens
  Categorizing Bugs Efficiently
  Here is a curated list of verified bugs in CRIU that make great candidates for open source contributions, ranked from beginner-friendly (good first issues) to
  intermediate.
  ──────
  ### 1. Memory Leaks in C API Options Cleanup (libcriu)

  • Difficulty: Beginner / Good First Issue
  • Location: criu.c:234-245 in criu.c:105-245
  • Problem: In criu.c:1170-1181 and criu.c:2152-2164, strdup() allocates copies of cgroup_yard and config_file. However, criu.c:105-245 never frees opts->rpc-
  >cgroup_yard or opts->rpc->config_file, causing a memory leak whenever options are re-initialized or freed.
  • Fix: Add free(opts->rpc->cgroup_yard); and free(opts->rpc->config_file); to criu.c:234-245.
  ──────
  ### 2. Clang Static Analyzer (scan-build) Header Build Break

  • Difficulty: Beginner
  • Locations:
      • bug.h:17-35
      • lock.h:13-19
  • Problem:
      1. bug.h:31-35 uses assert(!condition); when __clang_analyzer__ is defined, but <assert.h> is never included.
      2. In lock.h:13-19, LOCK_BUG_ON and LOCK_BUG are defined inside #ifndef __clang_analyzer__, leaving them completely undefined when running scan-build.
      This breaks scan-build compilation on almost every source file in the repository with undeclared identifier/function errors.
  • Fix:
      • Include <assert.h> under #ifdef __clang_analyzer__ in bug.h.
      • In lock.h:13-19, define LOCK_BUG_ON(condition) as assert(!(condition)) and LOCK_BUG() as assert(0) when __clang_analyzer__ is defined.

  ──────
  ### 3. Memory Leak & Uninitialized Packet Deinit in TLS Receiver

  • Difficulty: Intermediate
  • Location: tls.c:167-197 in tls.c:167-197
  • Problem:
      1. gnutls_packet_t packet; is uninitialized. If gnutls_record_recv_packet fails or encounters EOF on the very first loop iteration, the function breaks to err: and
      calls gnutls_packet_deinit(packet) on uninitialized stack garbage.
      2. For multi-packet transfers, gnutls_record_recv_packet(session, &packet) is called on every iteration, but gnutls_packet_deinit(packet) is only called once after
      exiting the loop. Every packet received prior to the final one is leaked.
  • Fix: Move gnutls_packet_deinit(packet) inside the while loop so every received packet is released immediately after its contents are written to the fd, and ensure
  deinit is called before returning on write errors.
  ──────
  ### 4. Memory Leak on Error Path in AppArmor Profile Dump

  • Difficulty: Beginner / Good First Issue
  • Location: apparmor.c:140-172 in apparmor.c:98-172
  • Problem: At line 140, cur->blob.data = xmalloc(sb.st_size); is allocated. If a subsequent read() fails or is short (lines 145-153), or if xrealloc(ns->policies, ...)
  fails at line 157, execution jumps to close: / err:. The err: cleanup only frees cur->name and cur, leaking cur->blob.data.
  • Fix: Add xfree(cur->blob.data); under the err: label in apparmor.c:168-171.
  ──────
  ### 5. Invalid List Pointer Usage in Cgroup Controller Collection

  • Difficulty: Beginner to Intermediate
  • Location: cgroup.c:676-698 in cgroup.c:660-751
  • Problem: In cgroup.c:660-751, the code searches for an existing controller with list_for_each_entry(cg, &cgroups, l). If no matching controller exists
  (!current_controller), the loop completes. At this point, cg points to an invalid dummy entry offset from the list head. Line 694 then calls list_add_tail(&nc->l, &cg-
  >l); instead of referencing the list head &cgroups.
  • Fix: Change list_add_tail(&nc->l, &cg->l); to list_add_tail(&nc->l, &cgroups);.
  ──────
  ### 6. Buffer Overflow Risk with sprintf in Process Seizing

  • Difficulty: Beginner
  • Locations:
      • seize.c:355 in seize.c:286-370
      • seize.c:490 in seize.c:440-509
  • Problem: Paths are constructed into fixed char path[PATH_MAX] buffers using unbounded sprintf(path, "%s/%s", root_path, de->d_name). Deeply nested cgroups or long
  directory names can cause a buffer overflow (similar to the cgroup buffer overflow recently fixed in commit dbdcd912e).
  • Fix: Replace sprintf with snprintf(path, sizeof(path), "%s/%s", ...) and check for truncation (ret >= sizeof(path)).
  ──────
  ### 7. Unhandled Missing PPID in crit ps Process Explorer

  • Difficulty: Beginner (Python)
  • Location: __main__.py:140-152 in __main__.py:129-153
  • Problem: When rebuilding the process tree for display, pp = pss[p.ppid] assumes every non-zero PPID exists in the dump. If a process had an external or undumped
  parent, pss[p.ppid] throws an unhandled KeyError. In addition, if psr is None, show_ps(psr, opts) crashes with an AttributeError.
  • Fix: Check if p.ppid in pss: before indexing, and handle multiple roots / orphaned tasks gracefully.
  ──────
  ### Tips for Submitting Your Contribution

  1. Linux Kernel Coding Style: Follow 8-space tabs for indentation, opening braces on newline for functions and same line for control blocks.
  2. AI tag: As required in GEMINI.md, include:
    Assisted-by: Gemini:3.7-Flash
  before your Signed-off-by line in commit messages.
  3. Run tests:
    make -j$(nproc)
    sudo ./test/zdtm.py run -t zdtm/static/env00


  Let me know which bug you would like to tackle first, and we can prepare the patch and test cases 