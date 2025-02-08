<h1>High-Level Design (HLD) Document: Multi-Region Deployment with Load Balancing :- </h1>
<b>1. Solution Diagram :-</b><p></p>

![Image](https://github.com/user-attachments/assets/a29e57a4-b872-43d4-8a36-3794e59a5ebf)

<b>2. Target Architecture Description :-</b>

<li>The application must be highly available and fault-tolerant through multi-region deployment by employing load balancers and database replication.</li>
<p></p>
(1) Multi-Region Deployment:-
<p></p>
<li>The application shall be deployed across two different regions for redundancy, say, Region 1 and Region 2.</li>
<li>Each region will have its respective load balancer, LB1 and LB2, respectively, to distribute the traffic within the region.</li>
<p></p>
(2) Global Load Balancer (GLB):-
<p></p>
<li>A global load balancer will route traffic based on latency and availability to the nearest or healthiest region.</li>
<p></p>
(3) Web Server Redundancy :-
<p></p>
<li>WebServerVM is replicated across both regions, serving static content.</li>
<li>In the event of regional failure, there will be automatic routing to another region.</li>
<p></p>
(4) Database Replication and Failover :-
<p></p>
<li>SQLVM configuration with primary in Region 1 and secondary replica in Region 2.</li>
<li>Data consistency across the regions is maintained by database replication.</li>
<li>It is behind the configuration of automatic failover to switch over to the secondary database in case of primary region downtime.</li>
<p></p>
(5) Redundancy and Failover Mechanisms :-
<p></p>
<li>Load Balancers: These ensure traffic distribution and avoid single-point failures.</li>
<li>Database Replication: Ensures data availability and consistency.</li>
<li>Automatic Failover: This minimizes the chances of downtown by automatically switching over to the secondary region during outages.</li>
<p></p>
<b>3. Migration Steps :-</b>
<p></p>
<b>The migration will be performed in the following key stages :-</b>
<p></p>
Step 1 : Replication of Virtual Machines Across Regions :-
<p></p>
<li>Creating a cloud-based VM replication service - AWS Application Migration Service or Azure Site Recovery.</li>
<li>Enabling real-time replication for WebServerVM and SQLVM to the secondary region.</li>
<li>Testing failover by simulating a regional outage.</li>
<p></p>
Step 2 : Configuration of Load Balancers :-
<p></p>
<li>Deploying a Global Load Balancer - AWS Route 53, Azure Traffic Manager - with routing policies :-</li><p></p>
	<ul>-> Primary Region Routing: US-East as primary, US-West as failover.</ul>
	<ul>-> Health Checks for the availability of web servers.</ul> 
<li>Using Local Load Balancers in each region to distribute traffic across multiple web servers.</li>
<p></p>
Step 3 : Database Replication and Failover Implementation Configure SQL Database Replication :- <p></p>
<li>AWS RDS Multi-AZ, Azure SQL Geo-Replication.</li>
<li>Creating an automatic failover mechanism for the SQLVM.</li>
<li>Testing failovers to make sure of seamless switching between primary and secondary databases.</li>
