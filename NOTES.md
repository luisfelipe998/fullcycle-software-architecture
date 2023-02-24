# Notes

Following along the full cycle software architecture course.

## Class 1: Types of architecture
Types:
- software: explained in further classes
- solution: explained in further classes
- technological: specialized in a certain tech. May have several technological architects inside the team with knowledge on different techs.
- corporate: Rules and constraints that impacts the company and development environment as a whole. Evaluates costs. Evaluates new techs. Standardizes techs.

## Class 2: Solution architect
Solution architecture: lies between the business and the software areas. Transforms business requirements in software solutions. Designs and represents how to solution will work (C4, UML). Evaluates commercial impacts regaring tech choices. May be envolved in pre-sales and sales stages. Evaluates costs of implementation and deployment.

## Class 3: Software architect
Software architecture: subject of software engineering. Related to software development. Affects the company organizational structure: teams, components. Relation between the business goals and constraints with the components and responsibilities aiming the software evolution over time. 

## Class 4: Software architect role
Roles:
- Transform business requirements into architectural patterns
- Orquestrate communication between devs and domain experts
- Undestand architectural concepts and models to find the best alternative to each challenge
- Support in decision-making under pressure
- Reinforce best practices
- Code reviews

Not all organizations have this role, if not, the dev senionrs and tech leads take over it.

## Class 5: Why learn software architecture
Reasons:
- Navigate between the macro and micro contexts withe ease;
- Undestand which is the best option to solve the problem at hand;
- Think on the long term and sustainability
- Less leaned to adopt market hyped tools
- Design Patterns and best practices
- Understand the software impact on the organization
- Take more confident decisions

## Class 6: Architecture vs Design
Architecture:
- Global scope
- Quality, high level constraints e business goals

Design:
- Local scope
- decisions to a component that are not visible outside of it

## Class 7: Sustainability on day zero
- is expensive
- solves an issue
- needs to pay off with time
- the costs over time have to be lower than the benefits it provides
- needs to follow the business evolution
- every software needs architecture

## Class 8: Software architecture pillars
- Structuring
- Componentization
- Relationship between systems
- Governance

## Class 9: Architectural requirements
How the requirements affects the architecture of the software.

Some categories:
- Performance: response time, throughput
- Data storage: where to store, how to store
- Scalability: horizontal and vertical, auto scalers
- Security: payments, personal data, cryptography
- Legal: compliance if laq
- Audit: logs, how much time store data, ensure security
- Marketing: Metrics about usage to impact users

## Class 10: Architectural features
Understand and have awareness about the architectural features of the solution, in order to solve problems intentionally rather than by luck.

Areas:
- operational
- structural
- cross-cutting

## Class 11: Operational
- **Availability**: how to manage it. SLA's. How critical the system is.
- **Disaster recovery**: how to recover when the system goes down. How to act. How to manage infrastructure downtime
- **Performance**: throughput and latency (response time). Design the system according to the performance requirements
- **Backups**: how it's done. Where it's stored. Test the backup.
- **Reliability & Security**: data traffic. Payment and personal data. Handle DDoS attacks. Handle brute force attacks. 
- **Robustness**: scaling up and down. Handle availability zone downtimes.
- **Scalability**: Horizontally e vertically.

## Class 12: Structural
- **Configurable**: connections, api keys, etc. The app should not be changed to run in staging or production environments.
- **Extensiblity**: New software (usually 3rd party) should be easily pluggable on the app.
- **Easily deployable**: standardization of envinroment: containers. Relates to configuration as well. How to manage dependencies that demands configuration (creation of tables, topics etc).
- **Reuse of Components**: Use the same libraries. Use the same layer of abstraction in different contexts.
- **I18n**: on backend: think which aspects will be affected (e.g. currency).
- **Easily maintanance**: take SOLID into consideration. Prefer the simple. Have good tests.
- **Portability**: Affect the application the least possible when changing a vendor dependency
- **Support**: Have consolidated logs, debugging, observability

## Class 13: Cross-cutting
- **Accessibility**: frontend libs to help with it
- **Data Retention & Recovery**: how many time maintain data. Do you have all the data you need? Do you need all the data you have? Tools: elasticsearch, prometheus
- **Authentication & Authorization**: Normally is used and Identity Provider. Or the system is behind an API Gateway that already handled the authentication
- **Legal**: Compliance with countries legal requirements
- **Privacy**: Keep the user data safe and private
- **Security**: Webfirewall (identify bots and OWASP attacks). Use the consolidated cryptography available. 
- **Usability**: Understand how to user consumes the application. In backend: API documentation and versioning. Standardization of responses.

## Class 14: Perspectives to architect software
- Performance
- Scalability
- Resilience

## Class 15: Metrics for performance
How the system behaves to handle a workload

- Latency (response time): time between the call and the response
- Throughput: how many requests the system can process

Performance != scalability

Points to improve performance:
- lower latency:
    - measured in ms
    - includes processing time, network and external calls
- Increase throughput:
    - more requests per second simultaneously
    - is related to latency

## Class 16: checklist to increase performance
Reasons to low performance:
- ineffective processing
- limited computing resources
- blocking calls
- serialized access to resources

Ways to increase performance:
- scale computing capacity (CPU, disk, memory, network)
- software logic (algorithms, queries, indices, framework overheads)
- concurrency and paralelism
- databases (types, schemas, understand which queries are bottlenecking the calls)
- caching

## Class 17: Scaling, concurrency and paralelism
- Vertical scaling: increase computational resources
- Horizontal scaling: increase number of app replicas and balance load with a load balancer or reverse proxy.

- Concurrency: handle several things at the same time (but doing one at a time)
- Paralelism: Do several things at the same time

Handle requests in a non-blocking way to process more requests (limited by the computational resources of managing multiple processing at the same time)

## Class 18: Caching
- Edge computing: server prior to the main server, with a cached copy of the necessary data, generally physically closer to the caller.
- Static data: images, css (can be cached with edge computing as well)
- Web pages: html, return cached data from previously processed request (avoid hitting the whole infrastructure and increase speed to user)
- Internal functions: cache data processed by a slow algorithm or database
- Objects: cache relations from database

Exclusive or shared cache:
- Exclusive: local on machine: low latency, duplicated between nodes. Session related issues (session will not be cached across all nodes).
- Shared: higher latency: access to central cache (external database). No duplication. No session related issues, because login data is stored centralized.

## Class 19: Cache vs Edge Computing
Edge computing: CDNs: keep the data closer to the user.

- Cache closer to the user (images, static files)
- Avoid requests hitting on cloud provider/infra
- CDN: content delivery network: replicate data across multiple datacenters. E.g. Akamai. Costs: access the content (hits on cdn) and band width necessary to replicate the data across its multiple points (mid grass).
- Cloudflare workers: edge computing platform. 
- Vercel: for frontend. 

## Class 20: Scalability
Ability to suport workload increases or decreases, with less or equal costs, in order to increase throughput.

- Vertical & Horizontal scaling

Prefer horizontal scaling. It may scale more and if one replica goes down, the others may still handle the workload

## Class 21: Scaling apps - decentralization
Horizontal scaling depends on the architecture of the system.

- Machines are disposable. They should be created and deleted seamlessly
- Ephemeral disk: ability to create and delete machines with no worries about losing data
- App server vs Asset server: related the ephemerality. Scale the app server that queries asset servers
- Centralized cache: related to ephemerality as well. The application doesn't store state permantly
- Sessions: related to ephemerality as well. different app servers should share the same session

## Class 22: Database scaling
- Increasing computational resources (vertically: limited)
- Segregate reads and writes: different databases with replicas
- Horizontal shards: create several machines (horizontal scaling) to allow reads and/or writes, called shards (replicas).
- Serverless: handl over the database challenges (including scaling) to the cloud provider
- Database otimization: monitor and undestand queries performance with APM (application Performance Monitoring). Check indices performance. 
- CQRS (command query responsibility segregation): split reads and writes 

## Class 23: Reverse proxy
Reverse proxy: server that lies in front of web servers that forwards the client requests to those web servers according to the defined rules.

Popular solutions:
- Nginx
- HAProxy
- Traefik

## Class 24: Introduction to resilience
It's the strategies to intentionally adapt the system when an error happens. It minimizes the risk of losing important data and/or transactions.

## Class 25: Resilience strategies
Protect and be protected.

- An app on a distributed system must have self protection mechanisms to ensure max operation.
- One app may not send more requests to another app than it can handle
- A running slow system is better than a down system

## Class 26: Health checks
- Way to verify the healthiness of the system
- Determine what should be done in case of unhealthiness
- An unhealthy system has a chance of recovery if traffic to it _ceases temporarily_. 
- Good health checks: don't return just a static response on a /health endpoint. More data and metrics should be collected (db access, avg response time) to assert the proper system health.

## Class 27: Rate limits
- Protect the system based on the limit it was designed to support
- Limit the amount of requests, if more requests are sent, they are blocked (return 500).
- Rate limits should not blindly block requests. Client preferences (e.g. IP addresses) should/may be defined to avoid critical systems being prevented to access your app.

## Class 28: Circuit breakers
- Protect the system by denying further requests in case of error, normally based on exceeding throughput (returning 500)
- States:
    - closed circuit: requests processing normally
    - open circuit: instant error
    - half-open circuit: allow a specified number of requests to validete if the system is back online
- May be implemented on code or on network

## Class 29: API Gateway
Centralize the receiving of all incoming requests, with powers to allow (and forward the request) or deny them.

- Authentication: ensures inappropriate requests don't reach the system. (e.g. Kong)
- May enable rate limis, health checks etc
- May transform payloads (xml to json)
- Headers enhancements

## Class 30: Service Mesh
Example: istio

It handles network traffic. Enable proxies between systems through side cars. All systems communicate with each other through these proxies. With that, we may get useful insights about networking.

It also avoid protection implementations by the own system:
    - retries
    - circuit breakers
    - rate limits
    - timeouts

It also cryptographes communications across you applications with the proxies (mTLS)

## Class 31: Async communication
- Avoid data loss: requests may await on a queue until it's possible to process it -> process more requests that would be possible in a sync way
- Requests are not lost if the system is down, by sending data to an intermediate that stores the data (message broker: queues)

Examples: rabbitmq, kafka

## Class 32: Ensure delivery with retry
A message may not always reach the destination service. A retry operation may be implemented. Retries should not be implemented linearly without backoff (resend the request with the same interval between them). The best implementation is the exponential (1, 2, 4, 8) with jitter. This will create a small noise between the intervals (2.05, 2.1, 2.25 ms), so many concurrent systems may have their retry requests processed in slightly different times.
There are several jitter implementations, with the best ones being the decorrelated and full-jitter with their trade-offs.

## Class 33: Ensure delivery with Kafka (brokers)
Acknowledging: different request message confirmations: Ack 0 (fire-and-forget: no one acks), Ack 1 (leader ack), Ack -1 (everyone acks). It will depend on the critically of the message (what are the issues if the message gets lost).

## Class 34: Complex situations
- What happens with the message broker is unavailable?
- Will you lose messages?
- Will your system be down?
- How to ensure resilience?

If we rely on the resilience of the broker, the broker turns into the single point of failure. Ask yourself: how handle it and how to manage costs of extra resilience?