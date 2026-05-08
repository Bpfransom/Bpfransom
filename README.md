<div align="center">
  <h1>Bpfransom</h1>
  <h3>Exploiting eBPF for Stealthier Ransomware
Attacks </h3>
    <p><small><i>Bpfransom is a stealthy eBPF-augmented ransomware that manipulates kernel-level observations to evade detection and neutralize defensive responses.</i></small></p>

</div>

⚡ Powered by [Aya](https://aya-rs.dev)🐝

## 💡 Overview
Bpfransom is a Rust implementation of offensive eBPF techniques that:

Feature Deception

1. blind I/O behavioral observation → inject error semantics into sensitive I/O operations
2. distort encrypted file content views → redirect read accesses to benign content
3. block HPC sampling processes → disable hardware performance counter collection


Remediation Disruption

1. hide target BPF programs & maps and ransomware processes → invisible to bpftool, bpftop, ps, top, procs, ls /proc ...
2. protect ransomware processes against tracing and termination → anti-tracing and anti-killing mechanisms

## 🚀 Artifact Description

### Akira
A traditional ransomware family used as a baseline target for evaluating eBPF-augmented evasive capabilities. **Decompression password: infected**

### BlackCat
A traditional ransomware family featuring advanced user-space evasion techniques, integrated for evaluating kernel-level enhancement effects. **Decompression password: infected**

### Luna
A traditional Rust-based ransomware sample used to assess compatibility with the eBPF adversarial component. **Decompression password: infected**

### ransompayload
The standalone ransomware encryption payload responsible for file encryption and attack execution.

### bpfransom_v1
The eBPF-augmented ransomware prototype that launches ransompayload and provides kernel-level stealth, feature deception, and remediation disruption capabilities.

### bpfransom_component
A reusable eBPF adversarial component that can be integrated into traditional ransomware families such as Akira, BlackCat, and Luna to enhance stealthiness, anti-analysis, and defense evasion capabilities.
