# Scheduled Reserved Instances
- Long term usage that doesn't run constantly
	- e.g Batch Processing daily for 5 hours starting at 23:00
	- Weekly data, sales analysis, every Friday for 24 Hours
	- 100 hours of EC2 per month

# Capacity Reservations
- Regional
	- Any AZ, billing discount for instances
	- No capacity in any AZ
	- Same priority as on demand
- Zonal
	- Only applies to 1 AZ
	- Capacity Reservation + billing discount
- On Demand capacity reservations
	- In 1 AZ
	- Paid for, even not used

# EC2 Savings Plan
- Hourly commitment for 1 or 3 year term
- Either for 
	- General compute $ amount ($20 per hour for 3 years)
		- Compute products - EC2, Fargate & Lambda
		- Those products have savings plan rate (up to amount that you commit)
		- Until you hit the commitment, then you use on demand rate
	- EC2 Savings plan - flexibility on size & OS