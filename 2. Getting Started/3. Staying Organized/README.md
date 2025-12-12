<h3>Staying Organized</h3>

Whether we are performing client assessments, playing CTFs, taking a course in Academy or elsewhere, or playing HTB boxes/labs, organization is always crucial. It is essential to prioritize clear and accurate documentation from the very beginning. This skill will benefit us no matter what path we take in information security or even other career paths.

<h3>Folder Structure</h3>

When attacking a single box, lab, or client environment, we should have a clear folder structure on our attack machine to save data such as: scoping information, enumeration data, evidence of exploitation attempts, sensitive data such as credentials, and other data obtained during recon, exploitation, and post-exploitation. A sample folder structure may look like follows:

htb[/htb]$ tree Projects/

Projects/

└── Acme Company

├── EPT

│ ├── evidence

│ │ ├── credentials

│ │ ├── data

│ │ └── screenshots

│ ├── logs

│ ├── scans

│ ├── scope

│ └── tools

└── IPT

├── evidence

│ ├── credentials

│ ├── data

│ └── screenshots

├── logs

├── scans

├── scope

└── tools
