Spark Perfromance Techniques :

**Join Strategies :  **
Spark decides what algorithm will be used for joining the data in the phase of physical planning, where each node u thelogical plan has to be converted to one or more operators in th ephysical plan using so-called strategies. the strategy responsible for planning the join is called join selection.

1. Broadcase Hash Join
2. Shuffle Hash Join
3. Shuffle Sort Merge Join
4. Cartesian Join
5. Broadcasted Nested Loop Join

**I. Broadcase Hash Join**

   ![image](https://github.com/user-attachments/assets/ca7b2c37-40fa-422b-b023-4487088f1b26)

Max size of dataframe that can be broadcasted. the default is 10 MB, which means only datasets below 10 MB can be braodcasted. <br>
**Spark.conf.set("spark.sql.autoBroadcastJoinThreshold")**

**joined_df.explain(extended=True)**
**joined_df.explain(cost=True)**

 In case, if you need to define explacitly define broadcast join then ,<br>

 **DfJoin = df1.join(broadcast(df2),df1.id== df2.id)**

Points to remeber : <br>
--> Broadcase Hash join is the fastest join algorithm when the following criterias are met :
     1. Works only for equi joins.
     2. Works for all joins except for full outer joins.
     3.Broadcast hash join works when a dataset is small enough that it can be broadcasted and hashed.
     4.Broadcast Hash join doesn't work well if the dataset that is being broadcasted is big.
     5.If the size of the broadcasted data set is big, it could become a netwrok intensive operation and cause your job execution to slow down.
     6.If the size if the broadcasted dataset is big, you would get an OutofMemory execption when spark builds the Hash table on the data.Beacuase the Hash table will be kept in memory.

**II. Shuffle Hash Join**
Shuffle join, as every shuffle operation, consists on moving data between executors. Shuffle Hash Join involves moving data with the same value of join key in the same executor node followed by Hash Join. Using the join condition as output key, data is shuffled amongest executor nodes and in the last step, the data is combined using Hash Join, as we know data of the same key will be present in the same executor.

![image](https://github.com/user-attachments/assets/d9a884d2-e7da-4a82-8815-408008a0adf5)

Points to remeber : <br>
1. Only supports for "=" join
2. this join will be picked whenever sort-merge join disabled (spark.sql.preferSortMergeJoin = False).
3. A single partition of given logical plan is small enough to build a hash table - small enough means here that the estimated size of Physical plan for one of joined columns is smaller than the result of spark.sql.autoBroadcasetJoinThreshold*spark.sql.shuffle.partitions. In otherwords, it's mostworthwhile to hash and shuffile data than to broadcast it to all executors.
4. Supported for all join types except full outer joins.
5. in my opinion, it's an expensive join in a way that involves both shuffling and hashing. maintaining a hash table requires memory and computation.
**
spark.conf.set("spark.sql.autoBroadcastJoinThreasold","-1")
spark.conf.set("spark.sql.join.preferSortMergeJoin","false")**

**Shuffle Sort Merge Join :-**

Shuffle sort-merge join involves, shuffling of data the same key with same worker, and then perfroming sort-merge join operation at the partition level in the worker nodes.

only supports for "=" join <br>
the join keys need to be sortable.<br>
supported for all join types.<br>

**spark.conf.set("spark.sql.join.preferSortMergeJoin","true")**

**Cartesian Join**
Cartesian Product join(a.k.a Shuffile-and replication Nested loop) join works very similar to a Broadcast Nested Loop join except the dataset is not broadcasted. <br>
Shuffle-and-Relication does not mean a "true" shuffle as in records with the same keys are sent to the same partition, Instead the entaire partition of the dataset is sent over or replicated to all the partitions for a full cross or nested-loop join.
works in both equi and non-equi joins
works only on inner like joins
This is very expecisive join algorithm, except load on the network and partitions are moved across the network.
High possibulity of out of memory exception.

**Broadcasted Nested Loop Join :-**
Broadcasted Nested Join works for by broadcasting one of the entaire datasets and perfroming a nested loop to join the data. So essentially every record from dataset1 is attempted to join with every record from dataset2. As you could guess, Broadcast Nested loop is not preferred and could be quite slow.

works for both equi and non-equi joins works for all join types.
Note that a sort is not involved in this join.




![image](https://github.com/user-attachments/assets/4bfef897-a13b-4c47-99d2-8025894861a0)



 
8. 
 
