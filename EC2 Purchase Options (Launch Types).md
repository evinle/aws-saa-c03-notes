# On-Demand
- Default - average of anything
- Per-second billing while instance is running
- Storage consumes capacity, billed regardless of instance state
- No interruption
- No capacity reservation
- Predictable pricing
- No upfront cost
- No discount
- Short term / unknown workloads
- Apps which can't be interrupted
![[Pasted image 20261004150410.png]]
# Spot
- You set a max price you're willing to pay
- When AWS has spares and is willing to allocate for your max price or below, it will charge you that rate
- If spot price raises higher, your instance is TERMINATED
- NEVER use spot for workloads which can't tolerate interruptions
- Non time critical
- Anything which can be rerun
- Bursty capacity needs
- Cost sensitive workloads
- Anything stateless

# Reserved
- Long term 
- Reduced or no p/s price
- Unused Reservation still billed
- Locked in type of instance & AZ or region
- Partial coverage of larger instance
- Reservations for 1 or 3 year

## No Upfront
- Reduced per/s fee
- Cheap

## Partial Upfront
- Reduced per/s fee
- Cheaper
## No Upfront
- No per/s fee
- Cheapest

![[Pasted image 20261004152939.png]]

# Dedicated Hosts
- Pay for host, designed for family of instances
- No instance charges
- Licensing based on sockets/cores
- ![[Pasted image 20261004153203.png]]

# Dedicated Instances
- Don't own or share the hosts
- Dedicated hardware
- One off hourly fee
- Dedicated instance fee separate
- ![[Pasted image 20261004153402.png]]
