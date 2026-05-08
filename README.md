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


## 🪄 Usage

Run `bpfransom` with root privileges:

```bash
sudo ./bpfransom --file <ransomware_binary> --target-args "<args>"
```

### bpfransom Parameters

| Parameter | Description |
|-----------|-------------|
| `--file` | Path to the ransomware binary under test. `bpfransom` attaches eBPF probes to monitor the target's system call behavior at the kernel level without interfering with its execution flow. |
| `--target-args` | Comma-separated arguments forwarded to the target binary at runtime, simulating the invocation conditions required by each ransomware variant (e.g., encryption scope, session credentials, target directory). |

> **Note:** Root privileges are required to attach eBPF programs to kernel tracepoints for system call interception.

---

### Ransomware Samples

| Binary | Description |
|--------|-------------|
| `ransompayload` | A self-developed ransomware prototype used as a baseline test case. |
| `0ee1d284...` | Real-world Akira ransomware sample identified by its SHA-256 hash. Accepts --id and --path arguments, indicating an ID-authenticated, single-path encryption workflow. |
| `3a08e3bf...` | Real-world blackcat ransomware sample identified by its SHA-256 hash. Requires an --access-token for authentication and supports path targeting via --paths. |
| `1cbbf108...` | Real-world luna ransomware sample identified by its SHA-256 hash. Operates in directory-sweep mode, encrypting all files under the specified -dir path. |

---

### Examples

**Self-developed payload — directory mode:**
```bash
sudo ./bpfransom \
  --file ./ransompayload \
  --target-args "-dir,/home/abc/Downloads/testfile"
```

**Sample `0ee1d284` — ID-authenticated, single path:**
```bash
sudo ./bpfransom \
  --file ./0ee1d284ed663073872012c7bde7fac5ca1121403f1a5d2d5411317df282796c \
  --target-args "--id,VDbAYZkdIB,--path,/home/abc/Downloads/testfile"
```

**Sample `3a08e3bf` — token-authenticated, multi-path:**
```bash
sudo ./bpfransom \
  --file ./3a08e3bfec2db5dbece359ac9662e65361a8625a0122e68b56cd5ef3aedf8ce1 \
  --target-args "--access-token,123,--paths,/home/abc/Downloads/testfile"
```

**Sample `1cbbf108` — directory sweep:**
```bash
sudo ./bpfransom \
  --file ./1cbbf108f44c8f4babde546d26425ca5340dccf878d306b90eb0fbec2f83ab51 \
  --target-args "-dir,/home/wangcheng/abc/testfile"
```
