**1. if you have to process 100 GB of data ? How will you decide the cluster configuration ?**

   Step 1:  Number of executer core required ?
   - we start by calculatin ghow many executor cores :
     One partition is of 128 MB of size by default ***
     - To calculate number of cores required, you have to calculate total number of partitions you will endup having
           100 GB = 100 * 1024 MB = 102400 MB
           Number of partitions = 102400/128 = 800
       Each partition required one core, i.e 800 - executor cores in total are required.

   Step 2: Number of executers required?
   Now that we have ho many cores/partitions , next we need to finc how many executers are required.

   - On an average, its recommended to have 2-5 executor coresin one executor
   - If we take number of executors cores in on executor = 4 then, total number of executors 800/4 = 200
   therefore, 200 executors are required to perform this task.

   Step 3:  Total executor memore required ?
   How much memore to be assigned to each executor:
   By default, total memore of an executor core should be 4 times (default partition memory) = 4*128 MB = 512 MB

   therefore, total executor memory = number of cores*512 = 4*512 = 2GB

   total memore required to process 100 GB data : executor has 2 GB of memory and total of executors= 200
   threfore, 400 GB of total minimum memory required to process 100 GB of data completly in parallel. 

 
**Summary :**
Number of Executors: 200
Cores per Executor: 4
Memory per Executor: 2 GB
Total Memory: 400 GB

<pre><code>
spark.executor.instances = 200                 # Number of executors
spark.executor.cores = 4                        # Cores per executor
spark.executor.memory = 2g                      # Memory per executor (2 GB)
spark.driver.memory = 2g                        # Memory for the driver (can be adjusted based on need)
spark.memory.fraction = 0.6                     # Fraction of heap space used for execution and storage
spark.memory.storageFraction = 0.5              # Fraction of memory reserved for storage
spark.default.parallelism = 800                 # Default parallelism (should be at least equal to number of partitions)
spark.sql.shuffle.partitions = 800              # Number of partitions to use when shuffling data
</code></pre>
