# Cyber-threats and Vulnerability Information Analyzer (CyVIA)
The standard risk assessment framework usually requires the use of tools or frameworks to collect data, followed by manual evaluation by cyber defenders to assess risk severity and determine if action needs to be taken. In contrast, CyVIA introduces a fully automated process that covers the entire risk assessment workflow, from data gathering to analysis generation. It enables continuous risk monitoring and provides threat-centric analytics that can adapt to changing network configurations without being restricted by time or space limitations. The key advantages of CyVIA include:

* Identify network and service dependencies within cyber infrastructures. 
* Evaluate individual nodes and the infrastructure as a whole for risk, taking into account implemented security controls and the risk from internal and external adversaries.
* Identify vulnerabilities within the operating systems and running applications of network nodes, and provide information on associated consequences and mitigation strategies.
* Classify the vulnerabilities based on type of weakness, severity, and access vectors.
* Infrastructure-based top 10 most vulnerable products.
* Highlight products based on mean severity, vulnerability scores, and number of vulnerabilities.
* Identify high-priority vulnerabilities and weakness types that defenders should prioritize for remediation.
* Generate relational analyses between the found vulnerabilities, products, and weakness types.
* Monitor for anomalous user activities based on recent adversarial trends.

### CyVIA Architecture:
<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/CyVIA_Full.png"><br>

### CyVIA Network Map
<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/network.PNG"><br>

### CyVIA Dependencies Map
<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/dependencies.PNG"><br>

### Results
We evaluate the proposed framework on a target network and discuss the derived results.

<img src="https://github.com/callmead/Risk-Assessment-VDB-Extension/blob/master/images/cve_relations.png"><br>

<img src="https://github.com/callmead/Risk-Assessment-VDB-Extension/blob/master/images/cwe-prods.png"><br>

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/CVEs_share_top10.png"><br>

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/CWEs_share_top10.png"><br>

### Setup Instructions:

You will need the following on your server machine:
* Graphviz 2.38 (should be available in the path environment variables)
* Flask 1.1.2 (for CyVIA API)
* Python 3
* CouchDB 3.1.1
* Jupyter Notebook

Requirements file:

aniso8601==8.0.0 <br />
certifi==2022.9.24 <br />
charset-normalizer==2.1.1 <br />
click==7.1.2 <br /> 
colorama==0.4.6 <br />
CouchDB==1.2 <br />
CouchDB2==1.13.0 <br />
Flask==1.1.2 <br />
Flask-RESTful==0.3.8 <br />
Flask-SQLAlchemy==2.4.3 <br />
idna==3.4 <br />
itsdangerous==1.1.0 <br />
Jinja2==2.11.2 <br />
joblib==1.2.0 <br />
lxml==4.9.1 <br />
MarkupSafe==1.1.1 <br />
numpy==1.23.4 <br />
pandas==1.5.1 <br />
pynput==1.7.6 <br />
python-dateutil==2.8.2 <br />
pytz==2020.1 <br />
requests==2.28.1 <br />
scipy==1.9.3 <br />
six==1.15.0 <br />
SQLAlchemy==1.3.18 <br />
tqdm==4.64.1 <br />
urllib3==1.26.12 <br />
Werkzeug==1.0.1 <br />

Jupyter Notebooks:
* 1_CWE_Master_Data_CouchDB.ipynb : Create Master Data for CWE referencing from MITRE.
* 2_Fetch_MITRE_CWE_CSV_Feeds.ipynb : Collect latest CWE feeds from MITRE. 
* 3_Fetch_NVD_JSON_Feeds.ipynb : Collect vulnerability data from NVD.
* 4_Prepare_Dataset.ipynb : Compile collected files and prepare CyVIA knowledgebase based on the found relationships between the data. 
* 5_Network_Scanner.ipynb : Scans network for nodes and open ports.
* 6_Dependency_Mapper.ipynb : Maps service and network dependencies between the found network nodes.
* 7_Control_Mapper.ipynb : Evaluates network nodes for applied security controls.
* 8_Process_Monitor.ipynb : Monitors running processes on network nodes.
* 9_Scheduler.ipynb : Responsible for scheduling jobs for keeping a check on updates and network activity.
* Node Analysis.ipynb : Evaluates each network node and prepares detailed report for each node. 

Other Python files:
* cyvia_api.py : API file
* agent_linux_v2.py : CyVIA agent for linux nodes to collect node information and pass to server agent.
* agent_windows_v2.py : CyVIA agent for windows nodes.
* client_scheduler_v2.py : CyVIA scheduler to keep agent timely running and communicating with server.
* server_scheduler_v2 : Server side scheduler to interact with client scheduler and keep server up to date.
* config.py : Server configuration.
* functions.py : Functions library for CyVIA.
* get-pip.py : If pip is not installed on your machine, you can use this file.
* process_scanner_v2.py : Process scanner for network nodes, works with the client scheduler file.
* Spinner.py : On Python notebooks if it is taking long time, the spinner spins to let the user know there is a process working in the background.

Script files:
* install_linux_req.sh : Installs required libraries on linux network nodes for the agent to work.
* install_windows_req.bat : Installs required libraries on a windows network node.
* linux_client_info.sh : Fetches linux network node information for the linux agent.
* win_client_info.psl : Fetches windows network node information for the windows agent. You may need to turn on the power shell execution on windows nodes, see Turn on scripts on windows.txt.

### Execution Flow:
* Deploy the agents on network nodes, ensure all nodes have Python and required libraries installed. Run the schedulers on nodes and the scan process will start. 
* On the server side, you may also run the server side scheduler. Once the client and server side schedulers start communicating with each other, the network node profiles will be created in CyVIA knowledgebase.
* After this, the individual Jupyter Notebooks can be run on need basis to see network analysis.

### Screen shots in action:
The programming language used is Python and we have used CouchDB as the backend. We are constantly upgrading the code, parts of the tool may not be available because of the continuous upgrades. As soon as we have a fully tested part, it will be available and screen shots will be provided as well.

CouchDB

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/CouchDB.PNG"><br>

At first, we collect CWE data from MITRE.

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/CWE_Collection.PNG"><br>

Then, we collect detailed information on these CWEs.

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/CWE_Details.PNG"><br>

Next we collect CVE Data from NVD Feeds.

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/NVD_Details.PNG"><br>

After this, we parepare the CyVIA Knowledge-base. 

<img src="https://github.com/trucyber/Risk-Assessment-Framework/blob/master/images/Prepare_dataset.PNG"><br>

<!--- <img src=""><br> ---> 

Read more on: 
* [Dynamic Risk Assessment and Analysis Framework for Large-Scale Cyber-Physical Systems](https://eudl.eu/doi/10.4108/eai.25-1-2022.172997)
* [Robust Cyber-threat and Vulnerability Information Analyzer for Dynamic Risk Assessment](https://ieeexplore.ieee.org/abstract/document/9647584)
* [Quantitative Risk Modeling and Analysis for Large-Scale Cyber-Physical Systems](https://ieeexplore.ieee.org/abstract/document/9209654)


# Quantitative Risk Modeling and Analysis for Large-Scale Cyber-Physical Systems
Threats of cyber attacks are very real today and greatly impact everything including the public health sector, economics, electric grids, internet of things (IoT), and national security. The number of new evolving threats and reported vulnerabilities has severely increased in the last few years. Perpetually refined cyber-attacks have set data, organizational assets, organizations, and individuals at considerable risk. Protecting sophisticated networks and interdependent systems, or reducing the impact of cyber-attacks has become a major challenge, where today’s effective countermeasures can be completely ineffective tomorrow. The various risk assessment frameworks and methodologies are either high-level, missing risk metrics values, not suitable for all kinds of networks, or publicly not available. To address this issue, we present a quantitative risk assessment model, that helps to model the organizational security posture, evaluates the security controls in place, and provides an understanding of the associated risks. We further provide a detailed explanation of the formulations and evaluate the proposed model on an industrial scenario.

<img src="https://github.com/callmead/Risk-Assessment-Framework/blob/master/images/RA-IoT%20(2).png"><br>


### Updates
We are in the process of refining and releasing code on the repository, contact the authors for more details and updated information.
