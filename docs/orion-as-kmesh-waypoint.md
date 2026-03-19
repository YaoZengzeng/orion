# Orion as Kmesh Waypoint: Replacing Envoy

---

### Why Orion over Envoy

| | Envoy | Orion |
|---|---|---|
| Language | C++ | Rust |
| Memory Safety | ❌ CVE-prone | ✅ Guaranteed by compiler |
| Performance | Baseline | **2–4× throughput** |
| Weight | Heavy (200+ deps, WASM runtime) | Lightweight, purpose-built |
| Kmesh-native | ❌ Requires patching | ✅ Native TLV/eBPF integration |
| Legacy burden | 10+ years, high change risk | Greenfield, optimizable |


### Replacement Status

- ✅ End-to-end validated in Kmesh cluster (Kind + Istio)
- ✅ xDS compatible — no control plane changes needed
- 🔄 Performance tuning & production stress testing in progress


### Vision: Kmesh + Orion

> **L4 by eBPF × L7 by Orion = Ultimate Service Mesh Performance**

eBPF handles L4 in-kernel with near-zero overhead.
Orion handles L7 in userspace with Rust-native speed and safety.
Together, they deliver **end-to-end extreme performance** across the full mesh stack.

---

## Speaking Notes

Orion is Kmesh's purpose-built Rust replacement for Envoy as the L7 Waypoint proxy. Compared to Envoy, the key advantages are performance, memory safety, a much lighter footprint, and the freedom to optimize specifically for the Kmesh use case — without carrying Envoy's decade of legacy complexity.

On replacement progress: the end-to-end path is already working — Orion runs in a real Kmesh cluster alongside Istiod, passes Gateway API conformance tests, and integrates natively with Kmesh's eBPF layer. The next phase is performance tuning and hardening for production.

The bigger picture is the combination: Kmesh already achieves extreme L4 performance via eBPF in the kernel. With Orion on the L7 side, we complete the picture — a service mesh where every layer operates at its theoretical performance ceiling, with no C++ safety baggage anywhere in the data path.
