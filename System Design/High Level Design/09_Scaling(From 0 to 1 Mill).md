# Scaling from 0 to 1 Million Users

## Step by Step Guide to Scaling from 0 to 1 Million Users

**1. Single Sever Setup :**

 - can serve single user easily(the types which we usually make in our college projects)
   ![Single Server Setup](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*7umoBkxqCQ32tBv4DrnHbg.png)

 - Requests will be coming from the User and our only Web server will be processing the request and serving the response


**2. Application and Database Separation :**

 - separating our design into web tier and data tier to scale our system a bit and to be able to serve more users.

 - web servers will be responsible for processing the requests and serving the responses and the database server will be responsible for storing the data.

**3. Load Balancer + Multiple App Servers:**
 - still after separation of the application and database, we can't serve a large number of users.

 - we can add multiple application servers to serve more users.(we can either scale horizontally or vertically , we will go by horizontal scaling since vertical scaling has certian limit(CPU, RAM, etc),SPOF(Single Point of Failure) and it is expensive)

 - we can add a load balancer to distribute the incoming requests to the multiple application servers.

 - A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set. The user connects to the public IP of the load balancer which further connects with the private IP of our defined servers.

 ![Load Balancer](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*KWRYdhS2UvBfh-aO7rT91A.png)

**4. Database Replication:**
  - till this point we have handled the problems of SPOF and single server overload through load balancer and multiple app servers.

  - but still, we have a single database server which can be a bottleneck(a SPOF).

  - we can add multiple database servers to handle more users.

  - Database replication can be used in many database management systems, usually with a master/slave relationship between the original (master) and the copies (slaves).

  - A master database generally only supports write operations. A slave database gets copies of the data from the master database and only supports read operations.

  - In most of the system , their is only one master(write operations are minimal) and multiple slaves(read operations are multiple and frequent).

  - this solves the problem of SPOF for data layer and gives us the ability to serve more users.
  - This very step offers these things :
      - `Better Performance` : Read operations can be distributed among multiple servers and write operations can be handled my master server.So the parallelism increases and the performance increases.
      - `Reliabilty` : If one server goes down, the other servers can still serve the requests.
      - `Availability` : If the master server goes down, the slaves can be promoted to master and the system can still serve the requests.

![Database Replication](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*7pgWTvPc9HqvxqhxTpc4Fw.png)

**5. Caching:**

 - we have handled the problem of SPOF for both application and data layer.

 - but still, we can't serve a large number of users because of the slow load/response time.

 - time to improve load/response time, we can use caching.

 - A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly. The application performance is greatly affected by calling the database repeatedly(Database operations are highly expensive). The cache can help in solving this problem.

- we can use a caching server like Redis or Memcached to store the frequently accessed data in memory.

- we can also use a CDN(Content Delivery Network) to cache the static content like images, videos, etc(next step).

![Caching](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*EX1K1fu7M-8biPf0L7yydw.png)


**6. Content Delivery Network:**

 - we have handled the problem of slow load/response time through caching.
 - but still, their is possiblity of caching more things such as static content(images, videos, etc).
 - we can use a CDN(Content Delivery Network) to cache the static content like images, videos, etc.
 - A CDN is a network of servers that are distributed geographically. The CDN caches the static content of the website and serves the content to the users from the nearest server.
 - This reduces the load time and increases the performance of the website.
 - The CDN also helps in reducing the load on the main server and helps in serving more users.

![Working of CDNs](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*eXFJdnQhrbX19UmuDtPaeg.png)


- System incorporates Cache and CDN to serve more users and to reduce the load time.

![CDN+Cache](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*J7Ot2lS7uifmZ-cKtZ8ilw.png)

**7.Stateless Architecture:**

- ouur architecture maintains the session state of the user in the server itself — So to authenticate a particular user, all its requests should go to its mapped server which stores its state.

- This adds an overhead on the server, also adding and removing servers becomes difficult in case of changing traffic.

- To solve this problem, we can make our architecture stateless. In a stateless architecture, the server does not store the session state of the user. The session state is stored in shared data store. 

- State data is stored in a shared data store and kept out of web servers. A stateless system is simpler, more robust, and scalable.

![Stateless Architecture](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*BJ5t8OhAe8ZNCAZZQHNe5w.png)

**8. Datacenter Distribution:**

- now we are becoming famous and now we want to also serve the users from different regions.
- we can distribute our data centers across different regions to serve the users from different regions.
- Deploy your application across multiple data centers or regions.
- Use global load balancers to route users to the nearest or best-performing data center.
- Implement data replication across data centers to ensure high availability and disaster recovery.  
- GeoDNS uses the IP address of the user from whom the DNS request is received, identifies the IP location, and serves a unique response according to the country or region of the user.

![GeoRouting and Datacenter Distribution](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*GR6HytU9LFAHa-tbgbZBqw.png)


**9. Messaging Queue:**

- we have handled the problem of serving users from different regions,SPOF,slow load/response time.

- but what if their need to be some background tasks(asynchronous in nature) which are time consuming and can't be done in the request-response cycle.

- we can use a messaging queue to handle the background tasks.

- A messaging queue is a form of asynchronous service-to-service communication used in serverless and microservices architectures. Messages are stored on the queue until they are processed and deleted.

- A message queue is a durable component, stored in memory, that supports asynchronous communication. It serves as a buffer and distributes asynchronous requests. 

- The basic architecture of a message queue is simple. Input services, called producers/publishers, create messages and publish them to a message queue. Other services or servers, called consumers/subscribers, connect to the queue, and perform actions defined by the messages.

![Messaging Queue](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*7G0cjuhEHiOYxdmk9wQ5PQ.png)

**10. Database Scaling:**

- again userbase increases and now we need storage so we scale our database.

- it can be done in two ways:
    - `Vertical Scaling` :  also known as scaling up, is the scaling by adding more power (CPU, RAM, DISK, etc.) to an existing machine. We can generally get highly powerful database servers say around 24 TB of RAM, these kinds of servers can store and handle lots and lots of data.Limitation includes: Restricted user base, higher risk of SPOF, and vertical scaling becomes highly expensive as you go higher to such powerful database servers.

    - `Horizontal Scaling` : also known as scaling out, is the scaling by adding more machines to your pool of resources. This can be done by adding more servers to your database. This is the most common way to scale a database. It is more cost-effective and can handle a large number of users.

   - `Sharding`(horizontal scaling) :
     - Sharding is a type of database partitioning that separates very large databases into smaller, faster, more easily managed parts called data shards. The word shard means a small part of a whole. Sharding is a way to spread the load of a database over multiple servers, improving the performance of applications.

     - Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the shard.

     - User data is allocated to a database server based on a particular sharding key. Anytime you access data, a hash function is used to find the corresponding shard.

     - Limitation includes Celebrity Problem, Joins, and Referential Integrity.(we will discuss these in detail in the next section)


**11. Logging , Metrics , Automatation and Monitoring:**

- Monitoring error logs is important because it helps to identify errors and problems in the system as our system and daily active users (DAU) grow.

- Metrics: Collecting different types of metrics help us to gain business insights and understand the health status of the system.

- When a system gets big and complex, we need to build or leverage automation tools to improve productivity. Each code check-in can be passed through some default checks and verified through automation, allowing teams to detect problems early. Besides, automating your build, test, deploy process, etc. could improve developer productivity significantly.


## Final Preview of the System:

- The final preview of the system(with taking all this in consideration) will look like this:

![Final Preview](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*f0SNyCSQmssBM8rNc3sfVw.png)




**Acknowledgements:**

- [Scaling from 0 to 1 Million Users](https://medium.com/geekculture/system-design-scaling-from-zero-to-millions-of-users-deca270ef784)
- Alex Xu - System Design Interview - An Insider's Guide
- Concept and Coding(HLD Playlist) by Shreyansh Jain




    


