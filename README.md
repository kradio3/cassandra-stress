# Docker composite for cassandra stress testing on 2GB RAM
Composite uses official cassandra image

## Change MAX_HEAP_SIZE
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
d685562c3c3b        196.70%             1.855 GiB / 2 GiB   92.73%              8.04 kB / 648 B     1.097 GB / 1.467 GB   268
```

## Stress results
```sh
Results:
Op rate                   :   16,830 op/s  [READ: 16,830 op/s]
Partition rate            :   16,830 pk/s  [READ: 16,830 pk/s]
Row rate                  :   16,830 row/s [READ: 16,830 row/s]
Latency mean              :    7.2 ms [READ: 7.2 ms]
Latency median            :    3.5 ms [READ: 3.5 ms]
Latency 95th percentile   :   25.4 ms [READ: 25.4 ms]
Latency 99th percentile   :   51.3 ms [READ: 51.3 ms]
Latency 99.9th percentile :   96.5 ms [READ: 96.5 ms]
Latency max               :  829.9 ms [READ: 829.9 ms]
Total partitions          :  1,000,000 [READ: 1,000,000]
Total errors              :          0 [READ: 0]
Total GC count            : 88
Total GC memory           : 13.722 GiB
Total GC time             :    4.2 seconds
Avg GC time               :   48.0 ms
StdDev GC time            :   65.7 ms
Total operation time      : 00:00:59
```
