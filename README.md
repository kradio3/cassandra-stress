# Docker composite for cassandra stress testing on 2GB RAM
Composite uses official cassandra image

## Change MAX_HEAP_SPACE
```sh
#look at etc/cassandra/cassandra-env.sh
cat etc/cassandra/cassandra-env.sh | grep MAX_HEAP_SIZE
```

## Run containter
```sh
#start composite
docker-compose up -d

#start containter statistics
docker stats
```

## Run stress test
```sh
#run container bash
docker exec -ti <cassandra-container> /bin/bash

#run write test
cassandra-container$ cassandra-stress write n=1000000

#run read test
cassandra-container$ cassandra-stress read n=1000000
```

## Resource loading
```sh
CONTAINER           CPU %               MEM USAGE / LIMIT   MEM %               NET I/O             BLOCK I/O             PIDS
d685562c3c3b        371.70%             1.855 GiB / 2 GiB   92.73%              8.04 kB / 648 B     1.097 GB / 1.467 GB   268
```

## Stress results
```sh
Results:
Op rate                   :   29,795 op/s  [READ: 29,795 op/s]
Partition rate            :   29,795 pk/s  [READ: 29,795 pk/s]
Row rate                  :   29,795 row/s [READ: 29,795 row/s]
Latency mean              :    4.0 ms [READ: 4.0 ms]
Latency median            :    1.8 ms [READ: 1.8 ms]
Latency 95th percentile   :   15.6 ms [READ: 15.6 ms]
Latency 99th percentile   :   29.8 ms [READ: 29.8 ms]
Latency 99.9th percentile :   58.2 ms [READ: 58.2 ms]
Latency max               :  698.9 ms [READ: 698.9 ms]
Total partitions          :  1,000,000 [READ: 1,000,000]
Total errors              :          0 [READ: 0]
Total GC count            : 66
Total GC memory           : 13.189 GiB
Total GC time             :    1.2 seconds
Avg GC time               :   18.0 ms
StdDev GC time            :    7.0 ms
Total operation time      : 00:00:33
```
