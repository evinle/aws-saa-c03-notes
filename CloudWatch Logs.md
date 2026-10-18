- Public, Regional Service 
- Endpoint to which applications connect to - in AWS Public Zone
- Store, Monitor, Access logs data
- Unified Cloudwatch agent to integrate with things from outside AWS
- Can generate metrics based on logs - *metric filter*


- **Log stream** - ordered set of log events, from a specific source, with a specific type of logging i.e VAR log messages
- **Log group** - container of multiple log streams, for the same type of logging, where we define
	- Retention settings, permissions, etc.
	- Metric filters
![[Pasted image 20260730192754.png]]

# Log Groups vs Log Streams
- **Log event** - one line: timestamp + message
- **Log stream** - ordered events from ONE source (one EC2 instance, one Lambda execution environment, one ECS task)
- **Log group** - streams of the SAME KIND of log, all sources
- One instance can write to several groups (one per log type), but gets one stream per group

```
                    ┌──────────────────────────────────────────────┐
                    │  LOG GROUP: /webapp/nginx/access             │
                    │                                              │
                    │  Settings live HERE (apply to every stream): │
                    │   • Retention: 30 days                       │
                    │   • KMS encryption                           │
                    │   • IAM / resource permissions               │
                    │   • Metric filters  ──► CloudWatch metric    │
                    │   • Subscription filters ──► Lambda/Kinesis  │
                    │   • Export to S3                             │
                    │                                              │
EC2 i-0aaa ──────►  │  ┌ stream: i-0aaa ───────────────────────┐   │
(CW agent)          │  │ 09:47:01 GET /      200               │   │
                    │  │ 09:47:03 GET /login 200               │   │
                    │  └───────────────────────────────────────┘   │
EC2 i-0bbb ──────►  │  ┌ stream: i-0bbb ───────────────────────┐   │
                    │  │ 09:47:02 GET /cart  500               │   │
                    │  └───────────────────────────────────────┘   │
EC2 i-0ccc ──────►  │  ┌ stream: i-0ccc ───────────────────────┐   │
                    │  │ 09:47:05 GET /      200               │   │
                    │  └───────────────────────────────────────┘   │
                    └──────────────────────────────────────────────┘

                    ┌──────────────────────────────────────────────┐
                    │  LOG GROUP: /var/log/messages  (OS logs)     │
EC2 i-0aaa ──────►  │   stream: i-0aaa                             │
EC2 i-0bbb ──────►  │   stream: i-0bbb                             │
                    └──────────────────────────────────────────────┘
```

## Why split
- Stream per source - keeps each source's events in order, not interleaved
- Group - configure once, every stream inherits (incl. future instances)
- Analogy: group = labelled drawer with rules on the front, stream = one server's notebook, event = a line in it

## Metric filter flow (group level, scans ALL streams)
```
LOG GROUP /webapp/nginx/access
   │  metric filter: pattern "[..., status=5*]"
   ▼
CloudWatch metric: Http5xxCount
   ▼
CloudWatch alarm: Http5xxCount > 10 in 5 min
   ▼
SNS notification / Auto Scaling action
```

## Exam PowerUp
- Retention set per **log group**, default = **never expire** → cost issue → set retention or export to S3 (+ lifecycle to Glacier)
- Metric filters, subscription filters, KMS encryption attach to **groups**, never streams
- Streams are auto-created - Lambda writes to `/aws/lambda/<function-name>`, new stream per execution environment
- Real-time processing (OpenSearch, cross-account) → **subscription filter** → Kinesis Data Streams / Data Firehose / Lambda
