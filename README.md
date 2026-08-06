# llama.cpp Source Snapshot

[![Language](https://img.shields.io/badge/Language-C%20%7C%20C%2B%2B-blue.svg)](https://isocpp.org/)
[![Build](https://img.shields.io/badge/Build-CMake-064F8C.svg)](https://cmake.org/)
[![Format](https://img.shields.io/badge/Model%20Format-GGUF-orange.svg)](https://github.com/ggml-org/ggml)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](llama.cpp-master/LICENSE)
[![Upstream](https://img.shields.io/badge/Upstream-ggml--org%2Fllama.cpp-black.svg)](https://github.com/ggml-org/llama.cpp)

A source snapshot of [`ggml-org/llama.cpp`](https://github.com/ggml-org/llama.cpp), a high-performance C/C++ inference engine for running large language models locally across a wide range of hardware platforms.

This repository preserves the upstream source tree inside the `llama.cpp-master` directory.

> This repository is not the official `llama.cpp` repository. For the latest features, fixes, documentation, and releases, refer to the [upstream project](https://github.com/ggml-org/llama.cpp).

## Features

The included `llama.cpp` source provides:

- Local large-language-model inference in C and C++
- GGUF model loading
- Low-bit model quantization
- Command-line inference through `llama-cli`
- An OpenAI-compatible server through `llama-server`
- CPU inference for x86, ARM, and RISC-V platforms
- Hardware acceleration through supported GPU backends
- Model conversion and quantization utilities
- Tokenization, sampling, grammar, and embedding utilities
- Benchmarking and validation tools
- Support for multiple text and multimodal model families

## Repository Structure

```text
llama.cpp-master/
├── llama.cpp-master/
│   ├── CMakeLists.txt
│   ├── README.md
│   ├── LICENSE
│   ├── include/             # Public C and C++ headers
│   ├── src/                 # Core llama.cpp implementation
│   ├── ggml/                # GGML tensor library
│   ├── common/              # Shared utilities
│   ├── tools/               # CLI, server, quantization, and benchmarks
│   ├── examples/            # Example applications
│   ├── tests/               # Test programs
│   ├── docs/                # Upstream documentation
│   ├── models/              # Vocabulary and model-related files
│   ├── grammars/            # GBNF grammar examples
│   ├── conversion/          # Model conversion modules
│   └── convert_hf_to_gguf.py
└── .vscode/
```

The actual build root is:

```text
llama.cpp-master/llama.cpp-master
```

## Requirements

A basic CPU build requires:

- A C++ compiler with C++17 support
- CMake
- Git
- A compatible GGUF model

Optional hardware backends may require additional SDKs, drivers, or development libraries.

## Building from Source

Clone the repository:

```bash
git clone https://github.com/nguyen-ky2910/llama.cpp-master.git
cd llama.cpp-master/llama.cpp-master
```

Configure and compile:

```bash
cmake -B build
cmake --build build --config Release -j
```

The generated executables are normally placed under:

```text
build/bin/
```

## Running a Local GGUF Model

Run an interactive prompt:

```bash
./build/bin/llama-cli \
    -m /path/to/model.gguf \
    -p "Explain the RISC-V architecture." \
    -n 128
```

Start an interactive chat session:

```bash
./build/bin/llama-cli \
    -m /path/to/model.gguf \
    -cnv
```

## Starting the Server

Launch the HTTP server:

```bash
./build/bin/llama-server \
    -m /path/to/model.gguf \
    --host 0.0.0.0 \
    --port 8080
```

The server exposes an API compatible with common OpenAI-style client workflows.

## Converting a Hugging Face Model

Install the Python requirements required by the conversion script, then run:

```bash
python3 convert_hf_to_gguf.py \
    /path/to/hugging-face-model \
    --outfile model.gguf
```

Conversion requirements and supported architectures may change between upstream versions. Consult the included upstream documentation before converting a model.

## Quantization

After producing an F16 or F32 GGUF model, use the quantization utility:

```bash
./build/bin/llama-quantize \
    model-f16.gguf \
    model-q4_k_m.gguf \
    Q4_K_M
```

Quantization reduces model size and memory bandwidth at the cost of some numerical precision.

## Useful Executables

| Executable | Purpose |
|---|---|
| `llama-cli` | Command-line inference and conversation |
| `llama-server` | HTTP inference server |
| `llama-quantize` | GGUF model quantization |
| `llama-bench` | Performance benchmarking |
| `llama-perplexity` | Perplexity evaluation |
| `llama-embedding` | Embedding generation |

The exact set of executables depends on the selected build options and source revision.

## Updating from Upstream

This repository currently appears to contain an imported source snapshot rather than a Git fork with preserved upstream history.

To maintain a customized derivative cleanly, consider:

1. Forking [`ggml-org/llama.cpp`](https://github.com/ggml-org/llama.cpp).
2. Creating a dedicated development branch.
3. Keeping custom changes in focused commits.
4. Recording the upstream commit used as the baseline.
5. Periodically merging or rebasing onto tested upstream revisions.

## Customization Status

No clearly identifiable custom FPGA, KV260, DMA, or external GEMM backend was found in the current repository snapshot.

If this repository is intended to contain a custom accelerator backend, document and commit:

- Modified source files
- New backend implementation
- CMake build option
- Supported tensor types and shapes
- Hardware initialization procedure
- CPU fallback behavior
- Validation results
- Upstream baseline commit

## Attribution

`llama.cpp` is developed and maintained by the contributors of the official [`ggml-org/llama.cpp`](https://github.com/ggml-org/llama.cpp) project.

This repository is maintained by [nguyen-ky2910](https://github.com/nguyen-ky2910) as a source snapshot for study and development.

## License

The included upstream source code is distributed under the MIT License. See:

```text
llama.cpp-master/LICENSE
```

Preserve the original copyright and license notices when redistributing or modifying the upstream source.
