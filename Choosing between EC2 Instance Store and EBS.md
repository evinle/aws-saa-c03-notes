# Instance Store vs EBS
- Persistence -> EBS
- Resilience -> EBS
- Isolated from instance lifecycle -> EBS

- Resilience w/ App in-built replication -> it depends
- High performance needs -> it depends
- Super high performance -> instance store
- Cost -> instance store (included)

- Cheap = ST1 or SC1
- Throughput ... streaming ... = ST1
- Boot ... NOT ST1 or SC1
- GP2/3 - up to 16000 IOPS
- IO1/2 - up to 64000 IOPS (\*256000)
- RAID0 + EBS up to 260000 IOPS (combined) (limited by instance itself) (io1/2 -BE/GP2/3) (needs large size instance)
- More than 260000 IOPS - instance store
- ![[Pasted image 20261003213035.png]]