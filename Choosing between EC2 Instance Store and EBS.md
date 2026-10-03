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