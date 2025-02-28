### 2. **Compile llama.cpp with ROCm + CPU Support**
Use the `Makefile` with HIP (ROCm) flags:
```bash
make clean && \
HIP_PATH=/opt/rocm \
CC=/opt/rocm/llvm/bin/clang \
CXX=/opt/rocm/llvm/bin/clang++ \
make -j LLAMA_HIPBLAS=1 LLAMA_CPU_OFFLOAD=1
```
- `LLAMA_HIPBLAS=1`: Enables AMD GPU acceleration.
- `LLAMA_CPU_OFFLOAD=1`: Allows splitting work between GPU and CPU.

---

### 3. **Run the Model**
Use the `--offload` and `--ngl` flags to split layers between GPU and CPU:
```bash
./main -m <model_path> \
  -p "Hello, world" \
  --offload 1 \
  --ngl <number_of_layers_to_offload_to_GPU>
```
- `--ngl`: Controls how many layers are offloaded to the GPU (e.g., `--ngl 33` offloads 33 layers to the GPU; the rest run on the CPU).
- Adjust `--split` to manage memory if needed.