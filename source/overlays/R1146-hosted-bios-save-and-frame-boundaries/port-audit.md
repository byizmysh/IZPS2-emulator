# IZPS2 inside a RUN25 .iza package

This audit was conducted locally and on Switch 2 with GTA San Andreas PAL, SLES-52541, CRC B440A8FE, and the `izps2-r799-gta-sa-entry.p2s` checkpoint. All device logs below use the EE, IOP, VU0, and VU1 JIT. Fastmem and MTVU are disabled.

| Area | Observed behavior | Changes and pending checks |
| --- | --- | --- |
| Package and code loading | R1133 returned `0xe606` when the segments were placed apart. Relaxing the required proximity of RX and RW allowed the loader to call the engine. | R1146 passed a local check of 39,964 relocations at displacements of ±32, +128, and −64 GiB. |
| BIOS, ISO, and GS resources | The previous paths differed from the SDK paths. Directory creation, BIOS lookup, and graphics resource loading had failed separately. | R1146 opened the BIOS and the same ISO on Switch 2, initialized Vulkan, and restored the checkpoint. |
| EE warm-up | R1143 read 65,616 bytes with status `ok`, validated 1,040 records, and prepared 1,024 blocks in 101.050 ms. R1144 and R1146 reached the first guest vblank with an empty initial dispatch entry, then began reading the profile. | The read path works. Further execution in the two deferred-warm-up runs remains unverified. R1146 recorded zero accepted image submissions at the first vblank. |
| EE profile and GS cache writes | The VFS opened the temporary file. Renaming, removing files, and listing the `sdmc:/…/cache` directory used libc. | R1145 and R1146 route these operations through the SDK. Local coverage includes preserving the old file after a publication failure, successful replacement, reopening, listing, and removing the temporary file. A profile write during a normal Switch 2 exit remains unverified. |
| BIOS settings | R1144 returned `errno 88` when reading NVRAM and MEC. Case-insensitive opening bypassed the VFS, and the BIOS directory is read-only. | R1146 stores support files under `saves/armsx2/firmware` and falls back to the existing copy beside the BIOS if a new copy is absent. This passed locally. The R1146 log contains no NVRAM or MEC errors. |
| Memory cards and saves | R1144 opened the card and loaded the checkpoint. The ZIP backup write failed on the libc path. | R1146 publishes the ZIP through the SDK and logged `MemcardBackup: backed up Mcd001.ps2` on Switch 2. Save State and Save and Exit still require an in-game check. |
| Diagnostic flags | Some options are read from `*.flag` files in the module root. The `HostVFS::stat` routes omit that directory for these paths. | Existing flag-driven tests need separate verification. Their settings should be set explicitly for each test. |
| Threads and logs | The SDK grants read access to child threads with `SB4_STORAGE_HOSTED_READ_SCOPE`. An earlier `runtime-latest.log` can remain on the SD card after a new container starts. | Use `emulog.txt` and the worker log for the active revision. Device checks still need to cover durable GS thread caches and reopening the same session. |

[R1143 emulog](../R1143-hosted-ee-entry-check/console-emulog.txt) · [R1144 worker log](../R1144-ee-warm-after-first-vblank/console-r1144-worker-start.log) · [R1146 worker log](console-r1146-worker-start.log) · [R1146 emulog](console-emulog.txt) · [Local storage model](storage-test.log) · [SD verification](console-app-deployment.json)

The R1146 tile, worker log, and game OSD identify the same build. Its `IZPS2_BUILD` entry in emulog still used the R1144 identifier. The R1147 control set both build identifiers.

Comparable gameplay windows were unavailable, so FPS improvement remains unmeasured.
