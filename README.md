**CONCLUSION:**
cloned the original JaxMARL-HFT training setup and conducted a controlled GPU vs CPU comparison on consumer hardware (HP OMEN laptop CPU=intel i7-13700HX GPU=Nvidia RTX 4060 Laptop).


CPU run was ~33% faster than the GPU run at NUM_ENVS=256, which initially appears to contradict the paper's 240x speedup claim.
However, this result is consistent with the paper's own experimental design: their benchmark allocated 64x more environments to the GPU (4096 vs 64) and used a datacenter-grade L40S GPU. The paper's speedup claim conflates raw compute speed with the ability to run more environments in parallel — a distinction our equal-envs comparison exposes.


key finding is that GPU acceleration on consumer hardware requires a minimum level of parallelism (likely NUM_ENVS > 512–1024) to outperform CPU. Below this threshold, JIT compilation overhead and GPU underutilisation eliminate any advantage. This is not stated in the paper but is implicitly supported by its choice of 4096 environments for GPU benchmarking.

Then the 1024 envs comparision benchmark was ran in which GPU out performed CPU
Credits : https://arxiv.org/abs/2511.02136
