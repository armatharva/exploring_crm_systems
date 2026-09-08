# Exploring CRM Systems Using Generative AI

## Student Information

- **Name:** Atharva Mudunuri (Ram)
- **Course:** ICS499 – Software Engineering and Capstone Project

## Executive Summary

For this assignment I used AI (mainly Claude, with some ChatGPT) to research CRM systems — what they are, why companies use them, how the major products compare, and how one would actually be built. I also tested a real open-source CRM (EspoCRM) and reflected on how trustworthy the AI's answers were.

## AI Tools Used

- **Claude** – used for most of the research (Parts 1-5)
- **ChatGPT** – used to double check a few answers

See [`prompts_used.md`](./prompts_used.md) for the prompts I used and how well they worked.

## CRM Research Findings

CRM (Customer Relationship Management) is software companies use to manage their interactions with customers — things like contacts, sales, marketing, and support. It started with paper records in the 1950s-70s and has evolved into cloud-based, AI-powered platforms today.

Companies use CRM for sales tracking, organizing customer info, marketing, customer support, and reporting. It solves real problems in industries like retail, healthcare, education, manufacturing, and nonprofits. The main modules are Contacts, Accounts, Leads, Opportunities, Activities, Tasks, Marketing Campaigns, Support Tickets, Reports, and Dashboards.

Full details in [`crm_research.md`](./crm_research.md) (Part 1).

## CRM Product Comparisons

I compared 5 commercial CRMs (Salesforce, HubSpot, Zoho, Microsoft Dynamics 365, Oracle NetSuite) and 4 open-source ones (SuiteCRM, EspoCRM, Odoo, Vtiger).

- **Most popular commercial:** Salesforce
- **Most mature open-source:** SuiteCRM
- **Best for a small business:** HubSpot (or EspoCRM if you want to self-host for free)
- **Best for a large enterprise:** Salesforce

Full comparison tables in [`crm_research.md`](./crm_research.md) (Part 2).

## Open Source CRM Evaluation

I explored **EspoCRM** using their live demo. It was easy to use with a clean interface and a nice drag-and-drop pipeline view, but it's missing things like advanced reporting and marketing automation compared to Salesforce or HubSpot. It would work well for a small or medium business but not a big enterprise.

Screenshots are in [`screenshots/`](./screenshots/). Full write-up in [`crm_research.md`](./crm_research.md) (Part 3).

## CRM Architecture Proposal

I also planned out how a CRM could be built using HTML/CSS/JS/Bootstrap, PHP, and MySQL:

- **Modules:** Login, Contacts, Accounts, Leads, Opportunities, Tasks, Reports, Dashboard
- **Database:** tables for users, roles, accounts, contacts, leads, opportunities, and activities
- **Libraries:** Bootstrap, jQuery, DataTables, Chart.js, PHPMailer
- **Security:** hashed passwords, prepared statements to stop SQL injection, escaping input to stop XSS
- **MVP:** just login, contacts/accounts, leads, a basic pipeline, and one dashboard — save marketing automation and support tickets for later

Full breakdown and diagram in [`crm_research.md`](./crm_research.md) (Part 4) and [`architecture/crm_architecture.png`](./architecture/crm_architecture.png).

## Prompt Engineering Examples

I logged 5 prompts and rated how well each one worked. The biggest thing I learned: prompts that asked for a specific format (like "make a table" or "give 5 examples") got much better answers than vague ones.

Full prompt log in [`prompts_used.md`](./prompts_used.md).

## Lessons Learned

1. AI is great for getting a fast overview of a new topic, but specific numbers (pricing, stats) need to be double-checked.
2. Being specific in a prompt gets a way better answer than a vague one.
3. Actually testing EspoCRM myself taught me more than just reading about it would have.
4. Building an MVP means deciding what NOT to include yet, not trying to do everything at once.
5. AI saved me a lot of time, but I still had to verify the important stuff myself.

## References

See [`references.md`](./references.md) for sources and what still needs verification.
