# Spray walls: a reduced ONNX Runtime build (size check)

2026-11-08 · Crux · for after 0.2.5, nothing in the app changes

**Question:** would an ONNX Runtime build with only the operators the hold model needs shrink the app's native libraries?

**Answer: yes, by more than half.** Built for speed like the official package, `libonnxruntime.so` goes from 34.2 MB to 14.5 MB: the APK gets about 8.4 MB smaller and the installed app about 19.7 MB smaller. Built for size it goes down to 11.7 MB, but runs the model more slowly.

## Numbers (arm64-v8a, the only ABI the app ships)

| | Official AAR 1.31.1 (in the app today) | Reduced, `Release` (built for speed) | Reduced, `MinSizeRel` (built for size) |
|---|---:|---:|---:|
| `libonnxruntime.so`, as installed | 34,208,672 B | 14,544,344 B (−57 %) | 11,661,896 B (−66 %) |
| `libonnxruntime.so`, compressed in the APK | 13,906,464 B | about 5,483,000 B (−61 %) | about 4,196,000 B (−70 %) |
| APK size saved | | about 8.4 MB | about 9.7 MB |
| Installed size saved | | about 19.7 MB | about 22.5 MB |
| Execution providers | CPU, XNNPACK, NNAPI (and more) | CPU only | CPU only |
| Operators | all | 44 `ai.onnx` + 6 `com.microsoft` | the same |

The app packs native libraries compressed and extracts them on install, so the APK (103 MB today) saves the compressed difference and the phone's storage the full one. `libonnxruntime4j_jni.so` stays about the same (about 92 KB).

## How it was built

- ONNX Runtime 1.31.1 from source, the same version the app uses, with the Android NDK for arm64-v8a: `Release` (and, for comparison, `MinSizeRel`), link-time optimisation, CPU execution provider only, telemetry not compiled in, no unit tests.
- `--include_ops_by_config` with an operator list taken from the hold model itself. The model has 2,266 nodes and uses 43 distinct `ai.onnx` operators at opset 17 (the int8 quantisation brings `ConvInteger`, `MatMulInteger` and `DynamicQuantizeLinear`; the rest includes `GridSample`, `Einsum`, `TopK`, `LayerNormalization`, `Erf`). The app opens the model with all graph optimisations on, and these fuse nodes into contrib operators (`DynamicQuantizeMatMul`, `FusedMatMul`, `Gelu`, `MatMulIntegerToFloat`, `QuickGelu`, `SkipLayerNormalization`), so the list holds the operators of the original model and of the optimised one.
- The build also produces the Java bindings (`onnxruntime4j`) as an AAR, so it could replace the Maven artifact one for one.
- One Android build of the reduced library took about 50 minutes; in CI it would only run when ONNX Runtime or the model changes.

## Does the model still run?

Yes, with identical results. The same operator list built for Linux (x86-64, `MinSizeRel` without link-time optimisation, with the Python bindings) loads the model with the app's settings (all graph optimisations on, CPU) and returns bit-identical boxes, scores and masks to the official ONNX Runtime 1.31.1 on four test tiles of a synthetic wall (12 output arrays, largest difference 0).

**The size-optimised build is slower.** `MinSizeRel` compiles for size (`-Os`). On the server it needed 2.6 s for the four tiles against 1.6 s for the official Python package (best of three runs, both at the app's settings). On the phone, where a photo takes about 12 s today, that could mean noticeably longer hold finding. That is why the `Release` build above is the one to compare. The same operator list built with `Release` for Linux (without link-time optimisation) also gives bit-identical outputs and needed 1.7 s for the four tiles against 1.4 s for the official package (best of three, two rounds), about 20 % slower; the `MinSizeRel` build needed 2.6 s. Part of the gap may come from the missing link-time optimisation and a different compiler on the server; the Android build has link-time optimisation on. How fast the reduced library is on the phone can only be measured with a test build of the app that uses it.

## What it would cost

- **A build in CI.** The reduced library is not on Maven; it would be built from the ONNX Runtime sources (MIT licence, the same notices as today) in a reproducible CI job and kept as a local AAR or a release asset with a pinned checksum.
- **Tied to the model.** A new hold model that needs an operator outside the list fails to load. The model check (`@Crux modellcheck`) would then also regenerate the operator list and rebuild the library before a new model can be pinned.
- **Tied to the settings.** The list covers all optimisation levels the app uses today. A different optimisation level or a new execution provider means a new list and a new build.
- **No XNNPACK or NNAPI.** The app runs the model on the CPU; XNNPACK and NNAPI are only options of the on-phone benchmark. A CPU-only build drops them; adding one back costs size that was not measured here.
- **Updates.** Every ONNX Runtime update (security fixes included) needs the build again.
