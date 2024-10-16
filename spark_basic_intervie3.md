****RDD, DataFrame and DataSet or Different types of Data Structures in Spark**

All of them are data abstraction APIs provided by Apache Spark for data processing and analytics. In terms of functionality, all are the same and provide the same output for any given input.<br>
They differ in terms of handling and processing data. They vary in performance, user convenience, and language support.<br>

Users can choose to work with any API while working with Spark.<br>

1) RDD - <br>
RDD stands for Resilient Distributed Dataset. An RDD is an immutable distributed collection of datasets partitioned across a set of nodes of the cluster that can be recovered if a partition is lost, thus providing fault tolerance. RDDs are Spark's fundamental data structure and provide a high-level API for performing distributed data processing tasks.<br>

Resilient - RDDs are immutable, partitioned collections of records that can be recovered if a partition is lost.<br>
Distributed - RDDs are a static set of items distributed across clusters to allow parallel processing.<br>
In-built memory computing - RDDs provide in-built memory computing and reference datasets stored in external storage systems.<br>

RDD provides an OOP-style API, and here we tell the Spark engine "How to do" basically, how to achieve any particular task. And, since here we tell the Spark engine how to achieve a task, optimization is in our hands <br>



2) Dataframes -<br>
DataFrames are distributed collections of data organized into rows and columns. The concept of DataFrames remains similar across all programming languages, but Spark DataFrames differ in functionality compared to Pandas. They are conceptually equivalent to a table in a relational database or a data frame in R/Python, but with richer optimizations under the hood.<br>

Since RDDs provide OOP-style programming, which can be somewhat challenging to work with, the DataFrames API was created to enable a broader audience to work with Spark. <br>

As an extension to the existing RDD API, DataFrames feature:<br>

The ability to scale from kilobytes of data on a single laptop to petabytes on a large cluster<br>
Support for a wide array of data formats and storage systems<br>
Seamless integration with all big data tooling and infrastructure via Spark<br>
APIs for Python, Java, Scala, and R (in development via SparkR) <br>

DataFrames provides SQL style API and here, we tell spark engine "What to do" and, spark engine will use optimization through the Spark SQL Catalyst optimizer to achieve the cost-effective way to accomplish the task.<br>



3) Datasets:
These are the newest data abstraction provided by spark. It is the combination of best of dataframes and best of datasets. It possess best of RDDs - OOP style + type saftety and best of Dataframes - structured format + optimization + memory management.<br>

Similiarity among all: <br>
Fault tolerant<br>
Distibuted<br>
In-memory paraller processing<br>
Immutable<br>
Lazy Evaluation<br>
Internally processed as RDD API<br>

Differences:<br>
Both RDDs and Datasets provide an OOP-style API, while DataFrames provide a SQL-style API.<br>
In RDDs, we specify to the Spark engine how to achieve a certain task, whereas with DataFrames and Datasets, we specify what to do, and the Spark Engine takes care of the rest. This is why DataFrames and Datasets inherently have optimization techniques.<br>
In RDDs, only on-heap objects are used, while in DataFrames and Datasets, both on-heap and off-heap memory can be utilized. Off-heap objects are employed when there is additional data in memory.<br>
Since RDDs use only on-heap objects, serialization is unavoidable because additional data needs to be transferred from RAM to disk. This is avoidable in DataFrames and Datasets due to the presence of off-heap space.<br>
In RDDs, *garbage collection (GC) impacts performance, but in DataFrames and Datasets, GC impact is resolved.<br>

*GC - Garbage Collector: When memory is full in RDD, GC will start scanning entire memory and it will start removing the data which is old and obselete.<br>

6) RDD and Datasets provide strong type safety that is at the time of you writing the code it'll give the error if something is wrong and thus they provide run-time compilation error. But, in the case of, DataFrames there's no type safety, so error will be known only once the code is executed and thus, they provides error at compile team.<br>

In summary, Apache Spark's trio of data abstraction APIs—RDDs, DataFrames, and Datasets—offers a flexible framework for distributed data processing. While sharing common traits like fault tolerance and in-memory parallel processing, they diverge in API styles, optimization strategies, and memory management. RDDs, with their OOP-style API, enable users to explicitly guide the Spark engine, whereas DataFrames, featuring a SQL-style API, focus on user-friendly interactions and seamless language integration. Datasets combine the strengths of RDDs and DataFrames, incorporating OOP style, type safety, and efficient memory handling. The choice among these abstractions hinges on specific task requirements, programming preferences, and optimization needs, highlighting Spark's adaptability in catering to diverse data engineering and analytics scenarios

**What is the benefit of using Datasets in Spark?**
Datasets provide compile-time type safety and object-oriented programming, which can help catch errors at compile time rather than runtime. This can improve code quality and reduce the likelihood of errors. Additionally, Datasets are faster than DataFrames as they use JVM bytecode generation for operations on data.






**Deployment modes in Spark| Client mode Vs Cluster mode:**

there are two types of modes in spark : 1. Client mode
                                        2. Cluster Mode

In client mode the drivier program will be created in edge node:
![image](https://github.com/user-attachments/assets/870acbc4-d913-47a3-9b9f-840a3257f706)

In cluster mode the driver program will be created in worker nodes. Spark will reuqest resources from resource manager and YARN will created Application manager in one of the worker nodes and same  nodes has driver program.

![image](https://github.com/user-attachments/assets/68f425b7-9d5b-49fe-a45c-f87b0c28790e)

