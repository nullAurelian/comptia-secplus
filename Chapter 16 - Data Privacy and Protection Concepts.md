Consider the people involved in Data Governance:
- Data Owner: senior with the ultimate responsibility of maintaining data confidentiality, integrity and availability
- Data Steward: role responsible for data quality, labelling and organizing data to be stored in a format and with values that are compatible with laws and regulations
- Data Custodian: manages the system that the data is stored on
- Data Privacy Officer: responsible for oversight of personally identifiable information (PII)
- Data Controller: responsible for determining why and how data is stored, used.
- Data Processor: entity that assist with collection, storage or analysis. Usually third-party.
Consider data life cycle:
- Collection: initial collection of data from users to servers
- Distribution: use of data across organization
- Retention: storage of data in organization
- Disposal: deletion of data after no longer useable
And Classification:
- Public (Unclassified)
- Confidential (Secret): typically restricted to those who need to know
- Critical (Top Secret)
- Proprietary: typically intellectual property
- Private/Personal: Information that pertains to a person or identity
	- Personally Identifiable Information
	- Personal Health Data
	- Customer Data
	- Financial Information: Things such as accounts, tax returns, payment card. Covered by PCI DSS for safe handling and storage.
	- Government Records
- Sensitive: data that could be harmful to owners if made public or prejudice perception (ie religious beliefs, trade union membership, etc). GDPR specifically defines this data type.
Paperwork for interacting with data:
- Privacy Notice: Must inform users that the data will be collected for stated purpose only. Purpose needs to be described clearly in plain language.
- Impact Assessment: Much like risk analysis, there should be an analysis on potential risks of collecting and processing data.
- Data Retention: Data that is to be stored should be backed up.
- Remember that different nations/states have different regulations and that data stored in those jurisdictions are subject to the regulations.
	- Data Sovereignty: That data generated in an area can only be used in that jurisdiction and cannot be stored or used outside or is heavily restricted.
Know where the data is:
- Data at Rest
- Data in Transit
- Data in Use
Minimize Data! Data minimization is the idea that only data that is needed for process should be collected or stored. Processes that need personal data should be documented so compliance can be proven. Once the process no longer needs the data, the data should be destroyed.
Anonymize data sets - PII/PHI should be decoupled from data where possible, hidden behind internal serial numbers or other generic data or fully anonymized to the point that reidentification cannot be done at all.
- Data masking: partially hide/replace data behind generic characters (typically 'x' or '\*') to redact sensitive portions while preserving the original data
- Tokenization: original data is stored in a database with a unique token associated with it. The token is shown to the outside while the real data is in storage.
- Banding/Aggregation: using generalized bands/segments rather than specific values (ie between 24-35 years old).
- Hash/Salting: like password encryption, hash/salt data
<h2>Dealing with Data Breaches</h2>
Understand immediate consequences:
- Reputation damage
- Regulation enforcement
- IP and Identity theft
Understand what to do in case of data breach
- Notify relevant parties based on laws and regulations.
	- May need to put out a public notification/disclosure of the breach.
- Escalate to senior decision-makers
- REMEMBER: YOU CANNOT OUTSOURCE ACCOUNTABILITY. Ergo, you should know what your partners are doing because it's your ass if you don't.
Data Loss Prevention: are products that automate the discovery and classification of data types and enforce rules to prevent exfiltration/unauthorized access.
- Policy Server: contains the rules that the DLP uses, logs actions and provides reports/summaries
- Endpoint Agents: (typically) a program that enforces policy based on Policy Server on endpoint devices
- Network Agents: (typically) a program that enforces policy based on Policy Server on a network
- DLPs can do certain automated actions to remediate a policy violation
	- Alert: incident is noted as a policy violation
	- Block: File is prevented from copying, but user can still access + Alert actions
	- Quarantine: File is denied to the user
	- Tombstone: Quarantine + file is replaced with one that describes the policy violation