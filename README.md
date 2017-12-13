CSD Project 2 Kirill Bogdanov 29/08/2017 
 
Interactive Visualisation System for Wide Area Network Paths 
1 INTRODUCTION 
Today, many popular cloud services are used by large numbers of users on a daily basis. These services are deployed on top of third party cloud services [1, 3, 2] and typically replicated across geo-distributed datacenters for reasons of survivability, reliability, and high performance. A large fraction of these important services are latency sensitive (in some cases meeting a fixed latency bound is critical). The quality of service (QoS), as perceived by the user’s is negatively correlated with latency. The perceived QoS directly affects user satisfaction and the overall revenue of a service provider (Amazon states that a 100 ms latency increase causes a loss of 1% of revenue [6]). 
For geo-distributed systems, network latency across a wide area network (WAN) can have a tremendous effect on the performance and responsiveness of a service. In WANs propagation delay can be the predominant effect on the overall network latency. Hence, understanding the network’s physical topology and exploiting this knowledge is important for geo-distributed services. 
In this project you will be given a large dataset containing network path measurements (produced by traceroute) performed among multiple geo-distributed datacenters of Amazon EC2. Your tasks will be to (a) analyse this dataset and identify statistical properties of these network paths, (b) design and develop a visualisation system that combines individual path measurements into a graph and project this graph onto the world map in an interactive fashion, (c) following your analysis you will design and develop an algorithm that will propose cost efficient infrastructure changes to the existing network topology. 
Required knowledge: Python, MySQL, Graph theory. 

1 
CSD Project 2 Kirill Bogdanov 29/08/2017 
2 EXAMPLE 
Figure 1 shows a network topology graph constructed from the dataset. This graph demonstrates various network paths between three datacenters of Amazon EC2 (i.e., Frankfurt (lower left corner), Oregon (lower right corner), and Tokyo (middle top). Blue vertices indicate datacenters, green vertices show identified IP addresses, gray vertices show unknown IP addresses, and red vertices show IP addresses common to network paths from Frankfurt to Tokyo and from Oregon to Tokyo. The width of edges indicates popularity of a given path segment. Single head arrows (i.e., edges) indicates the direction of the traceroute i.e., the source and destination datacenters. Due to the large number of the network paths that occur in the trace this figure shows only the 10 most popular paths for each pair of datacenters. 
Significant part of this project is to identify geographic locations of the important IP addresses and accurately place them on the world map. The importance of an IP address determined by its popularity and connectivity with neighbouring vertices of the network topology. The other should be placed with connecting vertices proportional to delay. 
Figure 1: Network topology between Amazon EC2 datacenters in Frankfurt Oregon and Tokyo. 

2 
CSD Project 2 Kirill Bogdanov 29/08/2017 
3 HIGH LEVEL TASKS 
Project divided into three logical phases. The first phase deals with data analysis, understanding, and interpreting of the dataset. The second phase deals with designing, developing, and setting up the visualisation system. The final phase, deals with development of an expert system that can analyse the data, suggest routing infrastructure changes (in accordance to specified constraints) and display the resulting infrastructure changes through the visualisation system. All phases and individual tasks require detailed descriptions in the project report. Note, Phases 1 and 2 are orthogonal to each other and can be executed in parallel. 
The following are high level tasks (grouped into three phases) in this project: 
1. Raw Data Analysis (total: 25%) 1. Demonstrate that the number of network paths between any two datacenters is finite (5%). 
2. Analyse persistence of network paths (5%). 
3. Extend measurement database with geographical information (10%). 
4. Correlate network latency with geographical distance (5%). 

2. Design and Develop Interactive Visualisation System (IVS) (total: 30%) 1. Research and choose a visualisation tool for the project (5%). 
2. Design and develop static IVS prototype (10%). 
3. Extend IVS to support run-time interaction (15%). 

3. Design and Develop Expert Infrastructure Change System (EICS) (total: 35%) 1. Design and develop EICS system (20%). 
2. Evaluate complexity of the EICS algorithm and its effectiveness (7.5%). 
3. Integrate EICS with IVS (7.5%). 

4. Remaining (10%) for documentation, code review, project maintenance, and planning. 

4 PHASE 1: RAW DATA ANALYSIS 
In this phase, you will learn how to interact with MySQL database and interpret network path information. Following after, you will perform data analysis to understand how individual measurements can be form into overall network topology. 
Task 1.1 (5%) Demonstrate that the number of network paths between any two datacenters is finite. The finite number of network paths can be demonstrated via analysis of the frequency of observing new paths between any 2 sampled endpoints (i.e., source and destination datacenters). This study expected to confirm existing work that demonstrates that path popularity is heavily skewed towards a few paths that are used predominantly and extend this earlier work by demonstrating that the same holds true for the private network of a cloud provider. 
Answer the following questions: For a given pair of source and destination datacenters, how often do we observe a new path that was not seen previously? What can we say about the probability of observing a new path, after considering measurements over 1 hour, 1 day, and 1 week? Are newly encountered paths used frequently? 

3 
CSD Project 2 Kirill Bogdanov 29/08/2017 
Task 1.2 (5%) Analyse persistence of network paths. In this task you will analyse how long a given network path persists. What is the average time that a network path persists? 
Task 1.3 (10%) Extend measurement database with geographical information. Research into techniques of IP geolocations. Agree on the format for the geographical data representation. Design and develop a script that connects to the traceroute database and extends it with tables/columns containing geographical coordinates. 
Suggested resources: 
• https://www.maxmind.com 
• https://www.maxmind.com/en/open-source-data-and-api-for-ip-geolocation 
• http://geobytes.com/iplocator/ 

Task 1.4 (5%) Correlate network latency with geographical distance. Analyse network distance among datacenters in terms of network hops, network latency and correlate it with the geographical distance. In this analyses answer the following questions. How many intermittent IP addresses are seen between any pair of datacenters? What are the longest and the shortest paths? Is the number of network hops correlated with the geographical distance between endpoints? 
4.1 PHASE 1 COMPLETION CRITERIA 
A successful completion of this phase requires production of the plots listed below, and write up explanation in the report. 
Task 1.1 
Produce 1 plot per pair of source and destination datacenters that demonstrates the frequency (or probability) of encountering new network paths with respect to time. 
1.1 Produce 1 plot that will aggregate the set of plots above in a single cumulative distribution function (CDF). 

Task 1.2 
Produce 1 CDF plot per pair of datacenters that show the average persistence of network paths. 

Task 1.3 
Demonstrate source code and the process of database extension. 

Task 1.4 
Produce 1 plot per pair of source and destination datacenters that shows the distribution of the number of network hops (i.e., hop distance). 
Produce 1 aggregate plot that shows the CDF of hop distances among all pairs of source and destination datacenters. 
Produce 1 plot showing correlation between number of network hops and geographic distance. 
Produce 1 plot showing correlation between network latency and geographic distance. 

5 PHASE 2: DESIGN AND DEVELOP INTERACTIVE VISUALISATION SYSTEM (IVS) 
Task 2.1 (5%) Research and choose a visualisation tool for the project. Consider all requirements and functionality necessary for the completion of this project. 
Note: make sure that selected visualisation tool can provide needed functionality. 

4 
CSD Project 2 Kirill Bogdanov 29/08/2017 
Suggested resources: 
• https://gephi.org/ 
• https://developers.google.com/maps/ 
• http://geoawesomeness.com/top-19-online-geovisualization-tools-apis-libraries-beautiful-maps/ 
• https://uber.github.io/ 

Task 2.2 (10%) Design and develop static IVS prototype. Following task 2.1, deploy visualisation tool of your choice and integrate it with the dataset. IVS should read network path information from the database, construct topology graph and display it on the world map. Therefore, IVS prototype should be able to produce a single graph (image) based on the static configuration. 
Implement the following requirements: 
• All measurement endpoints (i.e., datacenters) should be placed correctly at their geographic locations. 
• All identified IPs should be placed at the correct geographic locations. 
• IPs that are common for multiple trace directions must be highlighted as such. 
• The width of the edges should be proportional to the popularity of the given segment. 

Task 2.3 (15%) Extend IVS to support run-time interaction. Interaction can be implemented via graphical user interface (GUI) or via the terminal commands. 
Implement the following requirements: 
• Dynamically change source and destination datacenters that are being displayed. 
• Be able to display more than 1 pair of datacenters 
• Dynamically change the number of shown network paths (per pair of datacenters) based on their popularity. (e.g., display only top N paths per pair of datacenters). 

5.1 PHASE 2 COMPLETION CRITERIA 
Task 2.1 
Describe at least 3 visualisation approaches that you considered for this project in your report. Give more details for the tool that you choosed, justify your choices. 

Task 2.2 
Describe architecture and design of the IVS in the report. Demonstrate source code. 
Demonstrate a working prototype as per requirements. 

Task 2.3 
Demonstrate all required functionalities specified in the task. 

6 PHASE 3: DESIGN AND DEVELOP EXPERT INFRASTRUCTURE CHANGE SYSTEM (EICS) 
Task 3.1 (20%) Design and develop EICS system. In this task you will develop an expert system capable of proposing an alternative connections (routes) on the graphs based on the available information and available resources. 

5 
CSD Project 2 Kirill Bogdanov 29/08/2017 
Assumptions: 
• A1. It is possible to place additional vertices (network hops) anywhere on the world map and use these points to connect any number of existing neighbouring vertices. 
• A2. Network latency is proportional to the geographic distance as estimated in Phase 2 Task 2(a). 

Algorithm target: Minimize network latency between a set of datacenters. 
Subject to the following resource constraints: 
• C1. The number of vertices that is allowed to be introduce is limited (e.g., 1, 2, 3…etc.). 
• C2. The total distance of the new network links is limited (e.g., up to 10, 100, 1000 km etc.). 

Suggested resources: 
• https://blog.bixlyautomate.com/implimenting-a-rules-engine-in-python 
• http://pyke.sourceforge.net/ 
• http://pyclips.sourceforge.net/web/ 

Task 3.2 (7.5%) Evaluate complexity of the EICS algorithm and its effectiveness. Evaluate time requirements to find a solution as a function of the topology size and available resources. 
Task 3.3 (7.5%) Integrate EICS with IVS. Once EICS find a solution that satisfies the requirements it renders new vertices and edges of the network topology on the world map. 
6.1 PHASE 3 COMPLETION CRITERIA 
Task 3.1 
• Demonstrate source code in your repository containing the expert system. 
• Evaluate the benefits of using this EICS. Show at least 4 use cases where EICS can significantly reduce WAN latency given a minimum number of available resources. 
• Provide detailed description of the algorithm and the results it can achieve in the report. 

Task 3.2 
• Produce 1 plot showing dependency between average computation time versus variable topology sizes. Answer the question, is EICS scalable? 
• Produce 1 plot showing dependency between the amount of available resources and the WAN latency reduction achieved by EICS. 

Task 3.3 
• Demonstrate integration of EICS with IVS. 

7 READING MATERIAL 
Some references that might be relevant to you project: [4, 5, 7, 8] 

6 
CSD Project 2 Kirill Bogdanov 29/08/2017 
8 REFERENCES 
[1] Amazon ec2. http://aws.amazon.com/ec2/ Accessed 30-Nov-2015. 
[2] Google cloud. https://cloud.google.com/ Accessed 30-Nov-2015. 
[3] Microsoft azure. https://azure.microsoft.com Accessed 30-Nov-2015. 
[4] Brice Augustin, Xavier Cuvellier, Benjamin Orgogozo, Fabien Viger, Timur Friedman, Matthieu Latapy, Clémence Magnien, and Renata Teixeira. Avoiding traceroute anomalies with paris traceroute. In Proceedings of the 6th ACM SIGCOMM conference on Internet measurement, pages 153–158. ACM, 2006. 
[5] Attila Csoma, András Gulyás, and László Toka. On measuring the geographic diversity of internet routes. IEEE Communications Magazine, 55(5):192–197, 2017. 
[6] Greg Linden. Make Data Useful. https://sites.google.com/site/glinden/Home/-StanfordDataMining.2006-11-28.ppt. 
[7] Vern Paxson. End-to-end routing behavior in the internet. Networking, IEEE/ACM Transactions on, 5(5):601–615, 1997. 
[8] Himabindu Pucha, Ying Zhang, Z Morley Mao, and Y Charlie Hu. Understanding network delay changes caused by routing events. In ACM SIGMETRICS Performance Evaluation Review, volume 35, pages 73–84. ACM, 2007. 


