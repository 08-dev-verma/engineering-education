﻿### Introduction
Content migration involves moving content from one content management system to another. The process sometimes sounds simple, but it usually reveals areas of improvement in the site architecture, the design, and the content itself. 

If a redesign is needed, the migration process shifts from [lift and shift](https://cloud.netapp.com/blog/what-is-a-lift-and-shift-cloud-migration) to reorganizing and redesigning the architecture or content.

A typical migration involves redesigning information architecture, pages, content audit, new taxonomy, or even rewriting content. Sometimes migration may involve switching from one URL to another, posing many challenges. 

Most of these challenges can be solved using edge computing, which will be covered in this article.

### The concept of edge computing
[Edge computing](https://www.cloudflare.com/learning/serverless/glossary/what-is-edge-computing/) gradually changes how data is handled, processed, and delivered from millions of devices worldwide. The technology is rapidly growing due to the increased number of [IoT](https://www.zdnet.com/article/what-is-the-internet-of-things-everything-you-need-to-know-about-the-iot-right-now/) devices alongside the applications that require real-time data processing. Fast networking technologies like 5G networks support edge computing by creating real-time applications. These applications include video conferencing and processing, self-driving cars, AI, and robotics.

Edge computing was developed to address the issue of bandwidth costs for the data covering long distances. However, the rise of IoT-generated data real-time applications that require processing at the edge has made the technology grow faster.

Edge computing can be defined as distributed computing topology that processes information close to the edge. Edge, in this case, means where devices or people producing or consuming the information are located. The technology brings data processing and storage closer to the consumer devices rather than relying on a central location that is far away. 

Edge computing aims to ensure that the applications that use real-time data do not suffer from latency issues that significantly affect performance. This would save the organization's cost as the processing happens locally, hence no need for centralized or cloud-based locations.

Edge computing is crucial when it comes to content or data migration. Let us assume we manage a website that hosts huge content, such as thousands of articles. Then a need arises that we may have to change the website's domain name.

A challenge would arise on how we would redirect a million links from our old domain to the new domain. Typically to avoid the links from breaking, we can set a [redirect server](https://www.sciencedirect.com/topics/computer-science/redirect-server) that handles the traffic from the old domain and redirects them to the new domain. We can use edge computing to make tasks even easy and the whole experience better. Later sections will cover the issues that arise when migrating content and how better edge computing solves them and optimizes the system.

### Strategies followed to perform a successful content migration
This section will cover some of the best practices to be followed when performing a successful content migration. We usually follow an approach and checklist when migrating information in the system. The details may not be the same depending on the system and nature of information being migrated. However, the migration process always follows a general approach.

The typical content migration process involves strategy, planning, preparation, and migration phases, as explained further in the following paragraphs:

#### Phase 1: Strategy
This phase covers the following:
- **Reason for migration:** One reason may be that the current system may be no longer supported by the vendors, hence the need to migrate to the new system. Also, an organization may be planning to unify its systems for a better user experience. Whatever may be the reason, the change should impact the overall system.
- **Scope of migration:** It determines which information needs to be migrated. Suppose the organization is planning to do away with the whole old system. In that case, all information may need to be migrated. The organization should consider performing migrations in phases or targeting particular departments or processes for a file share cleanup. This stage impacts the timeline required to perform migrations.
- **The team involved:** A highly involved migration process requires commitment and resources from the organization. The top-level management in the organization needs to identify the need and allocate resources to the same. Afterward, then the team to be involved in migration can be determined. The migration team should at least involve business users, technical specialists, and information management specialists.

#### Phase 2: Planning
The next phase is to plan for the migration. This involves the following steps:
- **Source system inventory:** This step involves the information in the system, its metadata, and the way it is categorized or classified. Also, any relevant business rules or workflows and security settings are noted at this stage.
- **Source system key users:** In this step, the content users are noted. Also, the content owner and who will approve its migration is noted.
- **Source system information value:** This step determines the value of the information the source system holds. The checks on whether information can be recreated, redundant or obsolete are performed. The main reason is that organization would not migrate the information that adds no value to the business. Also, a business decision has to be made on which content to migrate and what to leave out.

#### Phase 3: Preparation
Up to this point, the plan is already laid out. The migration team can prepare for the actual migration of the content. The following tasks are to be performed:
- **Gather migration tools:** These are the tools that will be used in the migration process. They assist in identifying the proper folders and content to be migrated. They are also integrated with analytics to help classify the information. The team involved in migration should be prior trained to use the tools. Additionally, the tools also need to have been gathered before actual migration.
- **Analyze old and new system metadata needs:** Both old and new system metadata should be standardized. Folder structures should be prior analyzed and optimized correctly after migration.
- **Prepare target system:** The system key tasks need to be set up, such as security roles and settings, classification schemes, metadata set up, and workflows setup. Also, users need to be prepared to use the system once the migration is over.

#### Phase 4: Migration
After completing all the phases, the final phase involves the actual migration of the system. The steps may vary depending on the systems the organization is using. However, below are the guidelines:
- **Piloting and testing the migration process:** The process is first tried with relatively small data sets to ensure the correct approach. However, larger data sets should later be used to identify issues involved with such data.
- **Monitor migration:** As the migration process is proceeding, close monitoring should be made to identify any potential errors or issues associated with the process.
- **Perform quality control:** A quality technical check should be made to ensure correctness for every significant amount of content migrated. At this step, the users who are conversant with the information involved should contribute to ascertain whether the system is working.
- **Disabling access to the old system:** The access to the old system should be disabled instead of being deleted for some time. The reason is that some data might not have been successfully migrated due to legal or regulatory issues. However, it is helpful for the end-users not to access the old system once the migration process is over.

Content migration can be complex and not an easy task to undertake. It comes with some issues attached to it; some are technical. Most technical issues involved can be handled by edge computing, as covered in the following sections.

### Using edge computing to handle content migration issues
#### Latency issues
We will take a scenario whereby the servers are located in North America. Suppose a site visitor in Asia accesses the old URL. In that case, the request will travel to North America only to miss out on the resource requested. Then the redirect instructions will force the visitor back to where the resource is currently located. The browser will then send another request to North America to fetch the actual content on arrival. Finally, the visitor will access the original target. 

Below is the diagram that demonstrates the scenario:

![Latency](/engineering-education/using-edge-computing-to-handle-content-migration/latency.png)

The visitor requests content from the old URL, and the old server responds with the redirect instructions to the new domain. Then the web browser will send redirect instructions to the new domain. The response is then sent back to the site visitor.

The issue with the redirect chain is that the visitor has to wait for two round trips halfway across the world. However, using edge computing functions can significantly reduce the user's extra time to wait for redirect instructions.

Edge functions allow the developers to deploy serverless functions in any location around the globe nearest to the users. With the help of edge functions in handling the redirect requests, the initial user request would have instead interacted with the nearest edge server to fetch the redirect information.

We can use edge computing in the scenario we highlighted above. A site visitor in Asia would try to access the old URL. The request will only travel to the nearest edge server location, probably in the same city. The redirect instructions would still be in a different location. However, at least there is that information in the edge server. Once the browser sees the redirect instructions, everything will play as previously, only that the visitor does not have to wait long to access the content.

Below is a clear illustration of what happens with edge computing in place:

![Edge Compute](/engineering-education/using-edge-computing-to-handle-content-migration/edge-compute.png)

The site visitor requests the old URL. Then, the edge server, closest to the visitor, responds with redirect instructions. The browser proceeds to the new URL, and the response is sent back to the visitor.

#### Restructuring issues
Another issue familiar with content migrations is that the organization may need to change the URL structure for their blog posts. 

The organization might be comfortable changing their blog site from IDs to using the blog post title in the URL. For example, a blog post can appear as below:

`old-url.com/post/1`

The link to the same blog post can be changed to appear as below:

`new-url.com/blog/why-wordpress-is-important-as-cms`

The following is happening in the above links:
- The domain name and structure have changed.
- The blog post route `/post` has been changed to `/blog`.
- The blog slug for each post has been changed to use blog titles in place of the post ID.

Handling the above two changes is possible through [NGINX rewrite rules](https://www.nginx.com/blog/creating-nginx-rewrite-rules/) and [regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions). The third change can be challenging to handle since there is no way a program can map an old URL to a new URL.

We can try to solve the challenge by setting up a server that would take the requests from the old domain name. Then it would search for the needed post in a site database using a unique post ID. Next, it will create a new URL using the fetched blog post title and return the redirect information to the new URL.

However, the above will pose a few challenges. The database queries will add latency to the request and may be expensive to keep it running. 

We need to generate a one-to-one mapping of all the old web addresses to the new ones. This implies that every web address on the old domain will have a unique URL rewrite rule. A challenge comes if it involves many posts as it will bring much work.

However, one can create a one-time script during migration that loops through each database entry and automatically generates the rewrite rules. Unfortunately, the case would be identical if we use edge functions. We will still need to create one-to-one mappings, raising latency issues.

The critical difference is that web servers such as NGINX read the rules sequentially. This would mean that if we have 100,000 redirect rules and a visitor requests the last one. The server must loop through all the rules before reaching the desired rule to return the redirect information.

Edge computing offers [key-value storage](https://www.akamai.com/blog/news/now-available-edgekv-distributed-key-value-store). This implies that each of the 100,000 redirect rules will have O(n) complexity in the above scenario. In simple terms, it takes longer to reach the last item in the list as the items in the list continue to increase.

Edge's key-value storage devices come with an O(1) complexity. This means that no matter the number of items in the list, the look-up times will remain the same. 

We can save the URL mappings inside edge key-value storage in our previous example. Then edge functions can automatically check if there is redirect information in each request.

This would follow the below steps:
1. The user will request the old URL.
2. Then, the edge function near the user takes care of the request.
3. Next, using the edge function we will search for the redirect web address inside the edge key-value storage using the requested web address.
4. The user will get redirect information from the edge function.
5. The user will be able to access the new web address.
6. The new web address server responds to the request.

Using edge functions to handle the restructuring issues solves the latency issues. It also improves the performance for large-scale redirects where regex or wildcards may not make much impact.

#### Complexity issues
NGINX comes with added complexity for serving static assets, performing reverse-proxy, and balancing the load. However, a redirect server does not have to be complex. The complexity is much reduced when using edge computing, making developers more productive. Setting up and configuring an NGINX is complex and requires the developer to read through its documentation from time to time.

The advantage of edge computing is that it works with [serverless functions](https://www.pubnub.com/blog/what-is-a-serverless-function/), which are highly scalable. The developers need not worry about provisioning a server, the resources the server needs, or even the region to deploy the servers. 

With edge computing, developers write the functions, and the service provider decides where to run the code efficiently. It can scale accordingly to handle any additional load.

Performing redirects, deploying edge functions worldwide, and using the programming language that suits the developers to write the logic is efficient.

### Wrapping up
As we have already covered in the article, edge computing offers benefits when performing migrations and handling redirects. These benefits are:
- There is no time wasted while waiting for the requests to be fetched from a redirect server.
- There is minimal compute time required to process large URL mappings.
- There is less complexity involved in edge redirects than in provisioning and scaling a redirect server.

The future of edge computing for handling content migrations and performing large-scale redirects is auspicious.

### Further reading
- [A Guide to URL Redirection](https://www.semrush.com/blog/redirects/).
- [Creating NGINX Rewrite Rules](https://www.nginx.com/blog/creating-nginx-rewrite-rules/).
- [Faslty Edge Key Value Storage](https://docs.fastly.com/en/guides/about-edge-dictionaries).
- [Cloudfare Edge Key Value Storage](https://www.cloudflare.com/products/workers-kv/).
- [Akamai Edge KV](https://www.akamai.com/products/edgekv).