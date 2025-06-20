## 檔案簡介
### gem5
包含所有有修改的檔案，每個檔案都按照其路徑儲存
### Q3
#### 第三題的log
終端機輸出內容:
- `cmdlog_2-way.txt`
- `cmdlog_full-way.txt`
  
stats:
- `statsQ3_2way`
- `statsQ3_fullway`
### Q4
#### 第四題的log
終端機輸出內容:
- `cmdlog_FB.txt`
- `cmdlog_LRU.txt`

stats:
- `statsQ4_FB`
- `statsQ4_LRU`
### Q5
#### 第五題的log
終端機輸出內容:
- `cmdlog_WB.txt`
- `cmdlog_WT.txt`
  
stats:
- `statsQ5_WB`
- `statsQ5_WT`
## Questions
### Q2-Enable L3 last level cache in GEM5 + NVMAIN (15%)
#### 修改檔案
- `gem5/configs/common/Caches.py`
- `gem5/configs/common/Options.py`
- `gem5/src/cpu/BaseCPU.py`
- `gem5/src/mem/XBar.py`
- `gem5/configs/common/CacheConfig.py`
#### recompile gem5
```bash
        scons EXTRAS=../NVmain build/X86/gem5.opt
```
#### run hello world
```
./build/X86/gem5.opt configs/example/se.py \
-c tests/test-progs/hello/bin/x86/linux/hello \
--cpu-type=TimingSimpleCPU --caches --l2cache --l3cache --mem-type=NVMainMemory \
--nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config
```
### Q3-Config last level cache to 2-way and full-way associative cache and test performance (15%)
#### recompile gem5
```bash
        scons EXTRAS=../NVmain build/X86/gem5.opt
```
#### run
2-way
assoc = 2
```bash
        ./build/X86/gem5.opt configs/example/se.py \
        -c ./quicksort --cpu-type=TimingSimpleCPU \
        --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
        --l3cache --l3_size=1MB --l3_assoc=2 --mem-type=NVMainMemory \
        --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_2-way.txt
```
full-way
assoc = 16384
```bash
        ./build/X86/gem5.opt configs/example/se.py \
        -c ./quicksort --cpu-type=TimingSimpleCPU \
        --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
        --l3cache --l3_size=1MB --l3_assoc=16384 --mem-type=NVMainMemory \
        --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_full-way.txt
```
### Q4-Modify last level cache policy based on frequency based replacement policy (15%)
#### 加入檔案
- `gem5/src/mem/cache/replacement_policies/fb_rp.cc`
- `gem5/src/mem/cache/replacement_policies/fb_rp.hh`
#### 修改檔案
- `gem5/src/mem/cache/replacement_policies/ReplacementPolicies.py`
- `gem5/src/mem/cache/replacement_policies/SConscript`
- `gem5/configs/common/Caches.py`
#### recompile gem5
```bash
        scons EXTRAS=../NVmain build/X86/gem5.opt
```
#### run
```
./build/X86/gem5.opt configs/example/se.py \
-c ./quicksort --cpu-type=TimingSimpleCPU \
--caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
--l3cache --l3_size=1MB --l3_assoc=2 --mem-type=NVMainMemory \
--nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_FB.txt
```
```
./build/X86/gem5.opt configs/example/se.py \
-c ./quicksort --cpu-type=TimingSimpleCPU \
--caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
--l3cache --l3_size=1MB --l3_assoc=2 --mem-type=NVMainMemory \
--nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_LRU.txt
```
### Q5-Test the performance of write back and write through policy based on 4-way associative cache with isscc_pcm(15%) 
#### 修改檔案
- `gem5/src/mem/cache/base.cc`
#### recompile gem5
```bash
        scons EXTRAS=../NVmain build/X86/gem5.opt
```
#### run
```
./build/X86/gem5.opt configs/example/se.py \
-c ./multiply --cpu-type=TimingSimpleCPU \
--caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
--l3cache --l3_size=1MB --l3_assoc=4 --mem-type=NVMainMemory \
--nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_WB.txt
```
```
./build/X86/gem5.opt configs/example/se.py \
-c ./multiply --cpu-type=TimingSimpleCPU \
--caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=128kB \
--l3cache --l3_size=1MB --l3_assoc=4 --mem-type=NVMainMemory \
--nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config > cmdlog_WT.txt
```
