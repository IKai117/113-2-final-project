## Q2-Enable L3 last level cache in GEM5 + NVMAIN (15%)

## Q3-Config last level cache to 2-way and full-way associative cache and test performance (15%)
### run
2-way

```bash
        ./build/X86/gem5.opt configs/example/se.py \
        -c ./quicksort --cpu-type=TimingSimpleCPU \
        --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
        --l3cache --l3_size=1MB --l3_assoc=2 --mem-type=NVMainMemory \
        --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_2-way.txt
```
full-way
```bash
        ./build/X86/gem5.opt configs/example/se.py \
        -c ./quicksort --cpu-type=TimingSimpleCPU \r
        --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
        --l3cache --l3_size=1MB --l3_assoc=16384 --mem-type=NVMainMemory \
        --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_full-way.txt
```
## Q4-Modify last level cache policy based on frequency based replacement policy (15%)

## Q5-Test the performance of write back and write through policy based on 4-way associative cache with isscc_pcm(15%) 
