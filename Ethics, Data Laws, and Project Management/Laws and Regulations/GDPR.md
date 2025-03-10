|          Course Name          |      Topic      |   Professor    |         Date         | Tags |
| :---------------------------: | :-------------: | :------------: | :------------------: | :--: |
| **Data Laws and Regulations** | Data Protection | Julie Charpent | 27 & 28 février 2025 |      |
# Summary
*The GDPR is the landmark legislation in the EU which provides extensive data privacy and protection regulations for personal data. The stringent requirements under the GDPR come from the European philosophy that data is an extension of self and therefore enjoys rights to privacy. The GDPR applied [[AI Act|extraterritorially]] to anyone processing or controlling data in the EU as well as for any personal data of data subjects in the EU.*

# Key Takeaways
1. The EU views personal data as an extension of self compared to the US philosophy wherein it is considered property which can be sold
2. The EU Charter on Human Rights distinguishes between a fundamental right to data privacy and data protection
3. The scope of the GDPR is focused on the processing of personal data
4. Anonymized data is not considered personal data
5. The transparency principle expects that processing of data is transparent, understandable, and easily accessible
6. Under the GDPR, <mark style="background: #FFB86CA6;">personal data cannot be retained indefinitely</mark>
7. The FTC in the US found that an AI model trained on personal data cannot, by default, be considered itself to contain personal data
8. Individuals have the right not to be subject to fully-automated decisions
9. The principle of minimization reigns supreme and overrides even express consent

# Definitions
- Information: Insights and conclusions which can be drawn from data
	- Who you follow on Instagram is data but calculating the probability that you are a fan of a certain artist based on who you follow is information
- Express Consent: Active, explicit, and preferably written consent which must be free, specific, and informed
- Personal Data: one or more factors specific to the physical, physiological, genetic, mental, economic, cultural or social identity of that natural person
	- includes names, ID numbers, location data, online identifiers
	- Even sometimes can include IP addressed
- Processing: Any operation performed on personal data including collection, recording, organizing, structuring, storage, dissemination, ..., erasure
- Controller: The natural or [[Ethics and Laws Overview|legal person]]/entity which alone or jointly determines the purposes and means of processing personal data
- Processor: The entity which processes personal data on behalf of the controller
- Anonymization: A technique that irreversibly alters data so the data subject is no longer identifiable directly or indirectly
- Learning Phase: Designing, developing, and training an AI system and in particular, a model
- Production Phase: Operational deployment of the AI system obtained in the learning phase

# Additional Resources
- [GDPR Raw Text](https://gdpr-info.eu/)
- [GDPR Overview (Video)](https://www.youtube.com/watch?v=I-VuonciKWk)

# Notes
## Philosophies on Data Protection
- Many texts in the EU to discuss data protection
	- Founding treaties and the Charter
	- GDPR
	- Police Data Protection Directive (PDPD)
	- The e-Privacy Directive (ePD)
- The US tends to be sectorial and context-based in their approach
	- Property-like approach
	- Data protection is part of the right to privacy
	- Privacy doctrine principles (Daniel Solove)
		- Right to be left alone
		- Limited access to self
		- Secrecy - concealment
		- Control over personal informaion
		- Personhood - protection of identity, dignity
		- Intimacy
- The EU is more general and technologically neutral in their approach
	- Views data protection as a personal right of the individual
- Data is the only thing protected by the EU, however. Information gleaned from data is not subject to protection
- The GDPR was established under two main articles on the Treaty for the Foundation of the EU
	- Article 7: Respect for private and family life (includes communications)
	- Article 8: Protection of personal data
		- Everyone has the right to the <mark style="background: #FFB86CA6;">protection</mark> of personal data concerning him or her.
		- Such data must be <mark style="background: #FFB86CA6;">processed fairly for specified purposes</mark> and on the basis of the <mark style="background: #FFB86CA6;">consent of the person concerned or some other legitimate basis</mark> laid down by law. Everyone has the <mark style="background: #FFB86CA6;">right of access</mark> to data which has been collected concerning him or her, and the <mark style="background: #FFB86CA6;">right to have it rectified</mark>.  
		- Compliance with these rules shall be subject to control by an independent authority.
## Data Transfer Requirements
- Data transfer to a third country may only take place if the third country ensures an adequate level of data protection
	- The adequacy decision is given by the EU Commission
	- Individual companies may apply for a contract to export data and show that they have provided appropriate safeguards
- The adequacy decision is based on three criteria a third country must have
	- Similar legislation to the GDPR
	- Effective role of a control agency
	- Non-interference in data processing
## GDPR Scope
- Material Scope
	- The GDPR is focused on protecting the personal data of natural persons
		- Does not protect company data, dead people, or animals
		- Personal data must be able to identify (directly or indirectly) the specific physical, physiological, genetic, mental, economic, cultural, or social identity of a <mark style="background: #FFB86CA6;">natural person</mark>
		- If once can infer the identity of a natural person either from a single data point <mark style="background: #FFB86CA6;">or from crossing a set of data</mark>, it is personal data
	- Anonymized data is not considered personal data and is not in-scope for the GDPR
		- Cannot isolate some or all records which identify an individual
		- Cannot link at least two records concerning the same data subject of a group of data subjects
		- Not possible to deduce (with significant probability) the value of an attribute from the values of a set of other attributes
		- Pseudonymization is still considered personal data
			- Alias creation is a reversible process, unlike anonymization
- Territorial Scope
	- Controllers and processors in the EU even if the processing occurs elsewhere
	- Data subjects who are in the EU where the processing activities relate to
		- Goods or services irrespective of payment
		- Monitoring behavior which takes place in the EU
## Obligations Under GDPR
- All processing shall be collected for specified, explicit, and <mark style="background: #FFB86CA6;">legitimate purposes</mark>
	- Legitimacy is on a case-by-case basis
- The reasons for processing shall be <mark style="background: #FFB86CA6;">clear and transparent</mark>
- GDPR developer's guide from CNIL in France outlines ways to be compliant
	- Be aware of the core principles
		- Understanding the key notions around personal data, purpose, and processing
		- Recent decision stated that location and vehicle data (even technical) is considered personal data
	- Map and categorize the data processing
		- Duty to maintain a record of processing concerns, in principle, all entities, both private and public, regardless of their size, provided they process personal data
		- The mapping should be carried out with the Data Protection Officer (DPO)
			- A company must have a DPO if there are more than 250 employees in Europe
		- Sensitive data must be reported and have process recorded
	- Privacy Impact Assessment (PIA)
		- Done if there is a high risk to the rights and freedoms of natural persons
		- Must follow the principle of the <mark style="background: #FFB86CA6;">minimization of the data collection</mark>
			- Adequate, relevant and necessary in relation to the purposes for which they are processed, <mark style="background: #FFB86CA6;">as defined at the time of collection</mark>
		- There should be automatic deletion procedures including physical erasure of data and logging of the deletion event
- Collection of particularly sensitive data is prohibited without express consent
	- Racial/ethnic origin, political opinions, religious or philosophical beliefs
	- Trade union membership
	- Genetic & biometric data processed solely to identify a human being
	- Health-related data
	- Sex life or sexual orientation
- Duty to Inform Users
	- Data subjects are the only ones required to be notified
	- Must provide information on
		- Identity and contact details of the processor and controller
		- Purpose of the processing
		- Lawful basis for processing the data
		- Data retention period
		- Existence of the data subject's rights and the means to execute them
		- Contact details of the DPO (if applicable)
	- Must be provided in an easy-to-access way found with no difficulties and without the use of legalese, and all information should be in one document found on the website
## AI in the Context of the GDPR
- Purpose must be clearly-defined for development, training, and deployment and this objective must be determined at the design stage of the project
- Data protection requirements are not the same during the learning and production phases
- Need to establish a legal base for use still (@ least one)
	- Consent
	- Compliance with a legal obligation
	- Contract execution
	- Public interest
	- Safeguarding vital interests
	- Pursuit of a legitimate interest
- Datasets with long retention must not be to the detriment of the rights of the data subjects
	- The retention period should not be too long (cannot be indefinite)
	- Must determine and specify the retention period
	- For some industries and jurisdictions, retention periods are codified into the law
	- <mark style="background: #FFB86CA6;">Measuring performance over time is not, a priori, sufficient to justify long retention</mark>
- Need to safeguard from attacks
	- ChatGPT memorizing personal data and providing it as a query answer
- Need nest efforts for explainability but not a strict requirement
	- Document everything done in the model but not necessarily how decisions/outcomes were made/produced
- Allow data subjects to exercise their rights
	- Access, rectification, erasure, restriction, portability, and objection
	- Applied throughout the entire lifecycle of the AI
	- The processor may sometimes refuse the erasure
	- For fully automated decisions, individuals have the right to
		- know that it has happened
		- request to know logic and criteria applied
		- challenge the decision
		- request human intervention to review the decision
- Must avoid algorithmic discrimination