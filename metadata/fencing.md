
There is a feature in replicant which is called fencing. You would find a setting to enable/disable it in general config. That feature was built to fence a replication once started. There are two things metadata fencing and destination fencing. Metadata fencing means if there is a replication running with id repl1 using metadata1 then if you start another replication with the same id and the same metadata then it will fence it and the second replicant will not start detecting another replication with the same id.

If you run replicant with id repl1 and targetDB1 (tablesSet1) and metadata db as metadata1 then if you run another replicant with id repl1 and targetDB1 (tablesSet1) but metadata2 then metadata will not be fenced as metadata is different but destination is same so destination will be fenced.

To store the information related to fencing two tables are created, one in metadata db and another in target db.

default is enabled. If it is disabled then multiple replications can run with the same id and it will overwrite each other.   New replication will overwrite the progress of the old one and you will have to start from scratch. If you disable it then you would have to make sure you don't start replication with the same id.