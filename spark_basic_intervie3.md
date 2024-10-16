**Deployment modes in Spark| Client mode Vs Cluster mode:**

there are two types of modes in spark : 1. Client mode
                                        2. Cluster Mode

In client mode the drivier program will be created in edge node:
![image](https://github.com/user-attachments/assets/870acbc4-d913-47a3-9b9f-840a3257f706)

In cluster mode the driver program will be created in worker nodes. Spark will reuqest resources from resource manager and YARN will created Application manager in one of the worker nodes and same  nodes has driver program.

![image](https://github.com/user-attachments/assets/68f425b7-9d5b-49fe-a45c-f87b0c28790e)

