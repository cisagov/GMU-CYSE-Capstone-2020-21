## GMU-CYSE-Capstone-2020-21

### 1.0 Executive Summary 

This Request for Proposal (RFP) is focused on Anomaly Detection Analysis.   

### 2.0 Objectives 

Anomaly detection analysis is the subject of the proposed project. The desired deliverable is an integrated product that includes: 
 1. Algorithm for analyzing relevant data, 
 2. dashboard for visualization of the analytic results, 
 3. modeling documentation and user manual, 
 4. technical demo of the integrated capability. 

Dashboard, the primary output for this project, should have the capability to display the following: 
- Raw data input  
- Visualizations for the output 
- Capability to trigger alerts for a SOC analyst with a follow up action (i.e. analytic results to include recommended mitigations, e.g. close the port, disable the user account, quarantine the server, etc.) 

 
Prerequisites: 

- Knowledge of supervised (unsupervised preferred) machine learning 
- Knowledge of Log Analysis and time series data
- Knowledge of basic software application with web-server front end and database back-end 
- Knowledge of basic network traffic analysis


Students must be familiar with the principles of IT Operations and Security Analytics. Experience with log time series data in an operational setting is desired but not required.  Students should have a strong desire to learn how to safely and effectively conduct threat monitoring or threat hunting in the cloud and the role of machine learning. 

CISA team jointly with Elastic will provide all supporting documentation to bring the team up to speed on Elastic capabilities necessary for the project, but student team must establish and manage a student Elastic Cloud account.   

CISA technical SME will provide input on a starting dataset to seed the capstone research. However, it is anticipated the students will enrich their learning experience by seeking additional publicly available datasets or creating their own log files for analysis.  

### 3.0 Statement of Work / Requirements 

In order to develop the integrated dashboard for anomaly detection analysis, the team will perform the following: 

**Task 1** 

Find the following public datasets (or generate it from the built environment described below): 
- Outside the network looking for suspicious connections  
  - HTTP Proxy Logs (any open source proxy, students can choose) 
  - DNS Logs 
  - Netflow Logs 
- Inside the network looking for suspicious connections  
  - HTTP Proxy Logs (any open source proxy, students can choose) 
  - DNS Logs 
  - Netflow LogsLDAP logs (active directory) to let know which servers and users are behaving suspiciously 
  - CPU metrics logs to be combined with LDAP logs to validate suspicious behavior 
- Any other datasets that can support anomaly detection  

Potential sources for the datasets are:  
- Consume Mordor Datasets from here: AWS — The Mordor Project (mordordatasets.com). We chose mordor because they’re datasets are small and we want you all to focus on the structure. Download datasets individually, unzip them and verify JSON format - sometimes a file will fail - just download it again. Ingest though Kibana dev tools. Once ingested go to Kibana Discover and learn the dataset. 

Create a job using a single metric.   

If time permits explore classification, population, multi metric (more complicated and advanced) 
- https://www.kaggle.com/c/microsoft-malware-prediction 
- https://digitalcorpora.org/ 
- https://www.kaggle.com/datasets  

Please also explore the content of the DHS S&T project IMPACT: 
- https://www.dhs.gov/csd-impact, specifically https://ImpactCyberTrust.org/search.  

**Task 2**

- Build environment using Elastic Cloud (SaaS) is preferred.   
- Students will be provisioned student accounts to an Elastic cloud instance (Cloud UI).   
- Students will create a deployment for an Elastic Stack in their Elastic Cloud instance.  
- Students will select a cloud platform to host their deployment (AWS is preferred).  No additional cloud accounts required. 
- Students will select a region where their deployments will be hosted (cloud platform). 
- Students will pick a version of Elastic Stack (Elasticsearch cluster, Kibana, Beats and Logstash) or restore from a previous snapshot. 
- Students will add additional features; Machine Learning. 
- Students will utilize the following analytics software: 
   - Kibana visualizations and dashboards.  
   - Anomaly Explorer in Kibana  
   - Machine Learning in the Elastic Stack  
- Elasticsearch, Kibana, Logstash and Machine Learning in the Elastic Stack will serve as a starting point to support basic research at the beginning of the project.  

**Task 3**

- Ingest time series data into Elasticsearch indexes.   
- Students will utilize a combination of the following tools for data ingest: 
   - Kibana Dev Tools Console is the perfect fit for development and debugging.  
   - Elasticsearch Ingest Pipelines, Elasticsearch REST API or Elastic Search (ES) Python API scripts.  
   - Elastic Beats comes with Elastic. It is a set of lightweight data shippers that allow to conveniently send data to Elasticsearch Service.          Packaged with the Beats are modules that provide the configuration for data acquisition, parsing, indexing, and visualization for many common      databases, operating systems, container environments, web servers, caches, and so on. These modules provide a five-minute data-to-dashboard        experience.  
   - Logstash comes with Elastic. Logstash is a powerful and flexible tool to read, process, and ship data of any kind.   A common architectural        pattern is to combine Beats and Logstash: use Beats to collect data and use Logstash to perform any data processing that Beats are not            capable of doing. 
 - Students will define index templates with settings and mappings for the data attributes to be ingested.    

**Task 4**

- Build the dashboard in Kibana. 
- Design and implement data visualization(s). 
  - Add index patterns to Kibana. 
  - Add visualizations to Kibana and identify the best way to view results (Ex: Cluster graphs)  

**Task 5**

- Use anomaly detection to analyze time series data by creating accurate baselines of normal behavior and identifying anomalous patterns in your     dataset. Data is pulled from Elasticsearch for analysis and anomaly results are displayed in Kibana dashboards. 
- Create anomaly detection jobs to analyze datasets.   
- Use Anomaly Explorer and Single Metric Viewer to display results of anomaly detection jobs. 
- Separate operations datasets and security datasets.  Analyze machine learning (anomaly detection) results.  Find examples where you can you gain   deeper insights. 
  - Operations datasets: Elastic’s machine learning currently is focused on providing added value to time series data such as log files,               application metrics, system performance metrics, network flows, and other transactional data that can be collected and stored in                   Elasticsearch.  The key to getting good information is building a model of key indicators that occur with regularity throughout a data set.       When working with log data, some examples of regularly occurring key indicators would be HTTP status codes in Apache or Nginx web server           messages, or message codes in Cisco IOS messages. These key indicators occur regularly enough to be trended over a time period for the number     of times they occur. Metrics for memory utilization or duration counters are another example of regularly occurring key indicators. These         numerical fields can be averaged over a period of time so that the machine learning algorithms can model. It is best to use indicators that       stay fairly constant from one time period to the next, so it is important not to make the time period too small, where the indicators could       change significantly over a time interval. 
  - Security datasets: While threshold-based event notification is powerful, such as triggering a notification when a successful login is preceded     by multiple unsuccessful logins, the ability to automate the detection of anomalous behavior without having to define specific data conditions     simplifies the experience for the security analyst. That said, as we mentioned above, we're talking about mathematics, not magic, so the           machine learning engine must be given its marching orders as settings in its job configuration. Since the engine can model any type of time-       series data - numerical or categorical - the types of machine learning jobs that can be configured are unlimited. While this is flexible, it       can be a bit too much for a security analyst who really just wants to find threats. Here we introduce the concept of machine learning             "recipes" for security use cases. Recipes describe how to configure machine learning jobs, so that we can use automated anomaly detection to       uncover elementary attack behaviors that can be difficult to detect using other means. Elementary attack behaviors include activities such as     DNS tunneling, web data exfiltration, suspicious endpoint process execution, and more. 

**Task 6** 
- Design and implement “Alerts and Recommended Actions” capability: 
- Capability to map analytic results to mitigations or trigger alerts on the Kibana dashboard 

### 4.0 Customer Provided Materials and Information	 
DHS will provide technical support and information to enable this project to be successful.   

The following are references that will be provided to inform the project team. 

- Introduction to Statistical Learning: 
  - Introduction to Statistical Learning: by G. James, D. Witten, T. Hastie, and R. Tibshirani. (2013) | Springer Series in Statistics Springer New York Inc., New York, NY, USA | Retrieved from http://faculty.marshall.usc.edu/gareth-james/ISL/ISLR%20Seventh%20Printing.pdf 
     - Please see more resources accompanying this text here: http://faculty.marshall.usc.edu/gareth-james/ISL/ 
   - Python Machine Learning: by S. Raschka (2016) | Packt Publishing | Retrieved from www.PacktPub.com. 

- More advanced treatment of Statistical Learning: 
  - The Elements of Statistical Learning: by T. Hastie, R. Tibshirani, and J. Friedman. (2009) | Springer Series in Statistics Springer New York Inc., New York, NY, USA | Retrieved from  https://web.stanford.edu/~hastie/ElemStatLearn/ 
  - Advanced Machine Learning with Python: by J. Hearty (2016) | Packt Publishing   Retrieved from www.PacktPub.com 
     - www.PacktPub.com contains a lot of free resources on python coding, machine learning (supervised, unsupervised), deep learning, as well as additional manuals for Kibana and Elasticsearch (https://www.elastic.co/products/elastic-stack) 

### 5.0 Project Deliverables 

The contractor shall generate a project plan and propose deliverables that are appropriate for the project.  

The sponsor-specific desired deliverable is an integrated product that includes: 
  - algorithm for analyzing relevant data (i.e. Elastic’s out-of-the-box machine learning algorithm for anomaly detection), 
  - dashboard for visualization of the analytic results,  
  - modeling documentation and user manual,  
  - technical demo of the integrated capability.  
Please see previous sections for a more detailed description of the desired output and deliverables. 

The following technical approach is envisioned to accomplish the project. 
- Get data into the Elastic stack 
   - Raw input data (all the logs collected, and inputs used to support the analysis in JSON or CSV format) (mid Fall) 
   - Design and Build a Data Target in JSON format (map all data attributes of raw input data to the Elastic Common Schema) to use with index          templates  
   - Design and Build Kibana Index Templates 
   - Raw output deck (late Fall) 
- Modeling documentation (inputs, outputs, intermediate calculation steps explained) (early Spring) 
  - Design Kibana Index Patterns 
  - Design Kibana Visualizations 
  - Design Kibana Anomaly Detection Jobs 
- Integrated dashboard with data visualization, triggered alerts and mitigation recommendations (late Spring) 
  - Build Kibana Index Patterns 
  - Build Kibana Visualizations 
  - Build Kibana Anomaly Detection Jobs 
  - Design triggers (severity thresholds) that should trigger alerts. 
  - Create alerting on machine learning jobs that alert/notify users based on anomalies. 
- Technical demo of the integrated dashboard (late Spring) 

 
The following items must be included in this project as part of the course assignments.  

- CYSE 492/493 Deliverables 
  - CLIN-1 (Contract Line Item Number 1) Customer Reporting “Quad Pack”  
  - CLIN-2 Weekly Activity/Time Sheet  
  - CLIN-3 Color Team Briefing 
  - CLIN-4 Proposal (as a response to this RFP) 
  - CLIN-5 Design Review Briefing 
  - CLIN-6 Poster Paper 
  - CLIN-7 Final Report and Team Presentation 
  - CLIN-8 Product Specifications 

### 6.0 Terms and Conditions 

**6.1 Work Location**   

Projects will be performed at George Mason University, Fairfax, VA, unless other arrangements have been negotiated.  This includes virtual project work performed in remote student locations in accordance with current George Mason University policies and guidance. 

**6.2 Best Effort Basis**

This work scope is to be performed on a best effort basis. 

**6.3 Handling of Restricted Data**

Students, faculty, and administration are prohibited from signing any Intellectual Property agreements or Non-Disclosure agreements.  These are University policies and there are no exceptions.  No project work may include elements that are deemed For Official Use Only, Proprietary, Sensitive, or Classified.  Posters will be publicly displayed and Project Notebooks will be publicly available.  The Sponsor has the right to specify that their project team be comprised of US citizens; however, this does not imply allowance of Import/Export restricted information flow.  Students nor faculty nor administration can receive ITAR restricted information or data.  Should a company require approval of the Poster or other materials before public display, it is the responsibility of the Sponsor to ensure that such approval is secured in a proper and timely fashion and according to the requirements of the Sponsor's firm.  Sponsoring companies must assume widespread discrimination of provided technical and project information.  This includes other students, faculty, administration and even competitors in the marketplace as this is a totally open project.  In any event, GMU shall be held harmless for the public display of project materials.  

 
**6.4 Citizenship.**   

Does this Project require US Citizenship (Yes or No)?  

No. 

### 7.0 Proposal Guidelines and Requirements 

The student team shall provide a response to this RFP using the following outline: 

**Part 1 Technical Proposal**

Provide a detailed description of the project requirements, technical approach, and deliverables.  Use tables and figures to demonstrate your understanding and describe the approach.  Teams are encouraged to incorporate iterative, agile lifecycle approaches especially in cases where exact outcomes are difficult to define at the beginning of the project. 

**Part 2 Cost and Management Proposal**

At a minimum this section requires the following four items: 
  1. Organization Chart and Qualifications 
  2. Work Breakdown Structure (WBS) 
  3. Project Schedule 
  4. Project Cost - Weekly projected applied hours graph and estimated non-labor cost 

Examples are shown below.  Student teams must include the types of information shown but may modify format and add details as desired. 

a) Organization Chart and Qualifications Example 
 
![image](https://user-images.githubusercontent.com/84741121/121231936-01a57100-c85f-11eb-8ca9-918dc763b8bb.png) 

b) Work Breakdown Structure (WBS) Example shown below.  Students should construct a WBS that details the project plan.  Add additional levels of detail (sub-tasks) to fully define the project plan.  

![image](https://user-images.githubusercontent.com/84741121/121237136-b8f0b680-c864-11eb-9720-a9897096571b.png)


c) Project Schedule Example shown below.  Project schedules should align to the WBS.  

 ![image](https://user-images.githubusercontent.com/84741121/121232081-35809680-c85f-11eb-9018-86d813b51bec.png)

d) Project Cost 
  - Weekly projected applied hours (example graph) 
  - Estimated non-labor cost items separately.  This includes any software, cloud computing resources, or other non-labor items. 

![image](https://user-images.githubusercontent.com/84741121/121232191-55b05580-c85f-11eb-882f-7da6f888a1cd.png)

 
### Appendix A Customer’s Technical Specifications 
Additional technical specifications will be provided as necessary to inform the project work. 


### Appendix B Dataset additional resources
Lnks to help find the data: 
 - https://www.ncdc.noaa.gov/cdo-web/webservices 
 - https://webscope.sandbox.yahoo.com/ (account needed, free for university students and faculty) 
 - https://data.nasa.gov/browse?limitTo=datasets 

Use this Elastic blog and read about how they prepared the CTF environment:
 - https://www.elastic.co/blog/threat-hunting-capture-the-flag-elastic-security-bsides-2020  

Threat hunting capture the flag with Elastic Security at BSides SATX 2020 | Elastic Blog: https://www.elastic.co/blog/threat-hunting-capture-the-flag-elastic-security-bsides-2020. "Last month, members of the Elastic Security team hosted a threat hunting capture the flag (CTF) event at BSides SATX. We provided the community with an environment to learn and practice threat hunting with our team, and cultivated new relationships with attendees." www.elastic.co 

Preparing the CTF environment:
While designing the environment for the CTF, we decided to keep it relatively simple. We configured the following components, as shown in Figure 3: 
 - x1 Windows Server 2016 host configured as a domain controller 
 - x20 Windows 10 endpoints joined to the domain 
 - We installed several applications on each endpoint using Ninite in order to generate benign events and make the task of finding the flags in the dataset a bit more challenging for participants — after all, the goal of a threat hunter is to find the true threat amidst the noise 
 - Winlogbeat was installed on all endpoints and configured to ship Windows event logs, PowerShell logs, and Sysmon events to Elasticsearch. We used Olaf Hartong's popular sysmon-modular configuration with Sysmon 
 - Packetbeat was installed on all endpoints to ship network events to Elasticsearch 
 - All events were shipped to Elasticsearch running in an Elastic Cloud cluster 
 - Participants utilized Kibana to search and visualize the events indexed in Elasticsearch 
 - A CTFd platform was setup for participants to submit flags and score points during the event 

Use this Elastic blog and review how they setup another CTF environment with a known CVE - https://www.0ldmate.com/posts/tech/elastic-ctf-a2f4ee2043f5426e9233a5b318796535/  

Elastic CTF: "The Elastic CTF is a capture the flag competition that I built based on the Elastic Stack (formerly ELK Stack). I created it for the Sectalks Ninja Night as a way to give back something to the community that has given me so much. It was designed to give people a chance to play with a platform that is used quite often in security teams in many companies. This was my first time developing a CTF challenge and I hope I get the chance to do it again another time." www.0ldmate.com  

Focused on CVE-2019-7609:  "I installed an older version of the Elastic Stack (6.5.4) that was vulnerable to remote code execution (https://github.com/LandGrey/CVE-2019-7609) on the internal server and opened up SSH on the external facing server. I then simulated the attack from the attacker box making sure all logs are being sent to the Elastic Stack."


This is more forward leaning but gives you an idea of where we want to go once the teams understand the fundamentals: https://www.elastic.co/blog/embracing-offensive-tooling-building-detections-against-koadic-using-eql  

Embracing offensive tooling: Building detections against Koadic using EQL | Elastic Blog: https://www.elastic.co/blog/embracing-offensive-tooling-building-detections-against-koadic-using-eql.  This year at BSidesDFW, my local security conference, I highlighted a continuing trend of adversaries using open source offensive tools.The talk reviewed one of these post-exploitation frameworks named Koadic and walked through different ways defenders can build behavioral detections through the use of Event Query Language (EQL). In this post, I wanted to review this research by providing ...  www.elastic.co 
 
Consume Mordor Datasets: For next year…..  In anticipation for FY21-22 school year we need to discuss data generation before the end of the first semester - request focused guidance.  Also, in the near term, as it relates to data generation identify quick first steps (see below).   

Where to begin - quick first steps: 
 - Consume Mordor Datasets from here: AWS — The Mordor Project (mordordatasets.com) 
 - We chose mordor because they’re datasets are small and we want you all to focus on the structure. 
 - Download datasets individually, unzip them and verify JSON format - sometimes a file will fail - just download it again. 
 - Ingest though Kibana dev tools - Judy will demo this on Friday.  Once ingested go to Kibana Discover and learn the dataset. 
 - Create a job using a single metric.   
 - If time permits explore classification, population, multi metric (more complicated and advanced) 

Threat Hunter Playbook: https://threathunterplaybook.com/notebooks/windows/intro.html 
