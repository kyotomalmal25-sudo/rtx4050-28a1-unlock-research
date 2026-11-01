# RTX 4050 Laptop (10DE:28A1) experimental patch and MMA measurements

Supporting material for https://github.com/JustAResearcher/gpu-unlock-ada/issues/130. One machine and one successful unlock + RTD3-disabled boot; this is an experimental result, not a claim of broad device support.

* `28a1-tested.patch`: original tested patch against upstream commit d28c485418c3d9d034cd4bac19200bc33dd3453b. Comments describing hardware as unvalidated reflect when the patch was written; the subsequent tests and limitations are described in the issue. The patch requires the existing experimental opt-in and exact PCI target; it does not remove safety checks.
* `probe-8.cubin`, `probe.cu`, `worker.py`: saved 8-chain microbenchmark binary, source, and runner. The cubin SHA-256 is `3aebc6026e49f92fb857e12b420d7054374beb3d91b236d929e1474cc18965e2`. The source was preserved with the run; a reproducible binary build from this source has not been independently verified here.
* `stock/` and `unlock-rtd3-off/`: anonymized measurement, validation, preflight and monitoring records from independent boots. Five per-mode samples, 10 warmups, 1056 blocks x 256 threads, 20000 iterations, 8 chains, sm_89, FP32 accumulation, NVIDIA 615.71.09. Each mode verified 270336 output cells with zero mismatches.
* `power-management/`: anonymized PM samples and checks for the unlock + RTD3-off boot. Samples are discrete; intervals before the first sample and between samples are unobserved.

GPU and boot identifiers and local paths have been removed or replaced in the copied JSON. Original files were left intact. For this reason, saved original hashes in manifests may not match the anonymized copies. File contents retain monitoring artifacts including missing or implausible power readings; they are not substituted with assumed values.

Stock vs unlock + `nvidia.NVreg_DynamicPowerManagement=0x00` medians were respectively 24.015 vs 47.849 TFLOPS FP16, 24.015 vs 47.850 BF16, and 12.008 vs 23.926 TF32. Both are separate boots and this is a descriptive comparison. Some FP16 clock samples were low and stock FP16 monitoring included SW power/thermal-active samples. The benchmark host windows include warmup and verification; their overlap with individual CUDA event intervals is unknown.

The stock + RTD3-off control was not completed. Unlock and the power-management setting changed together, so neither unlock alone nor a D3cold mechanism is established. No independent successful-boot repetition, application speedup, or long-term stability claim is made. See the issue for context and requested follow-up.

The stock/, unlock-rtd3-off/, and power-management/ directories and probe source are inside the downloadable anonymized-measurements.zip archive.
