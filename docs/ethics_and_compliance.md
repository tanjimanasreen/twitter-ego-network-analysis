# Ethics, Privacy & Platform Compliance Statement

## 1. Compliance with X (Twitter) Developer Policy

This repository strictly abides by the **X (Twitter) Developer Agreement and Policy** regarding the redistribution of Twitter Content:

* **No Redistribution of Raw Content:** In accordance with platform guidelines, raw scraped tweet text, full user profiles, biography strings, and identifiable user screen names are **not redistributed** in this public repository.
* **Academic Sharing Guidelines:** For academic research reproduction, platform guidelines specify that datasets should share tweet identifiers or aggregated/anonymized feature tables. Researchers wishing to re-hydrate original tweets can do so using the official X API v2 endpoints via the provided scraper script.
* **Respect for User Rights:** Because social media users may choose to delete tweets, make their profiles private, or delete their accounts, redistributing static offline archives of user tweets circumvents user consent and platform deletion cascades.

---

## 2. Protection of Sensitive Personal & Health Data (IRB / Ethics Standards)

Research exploring mental health discourse on social media requires ethical data stewardship:

* **Special Category Data:** Under international privacy regulations (including GDPR Article 9 and human subjects research protections), data concerning an individual's physical or mental health is classified as sensitive personal data.
* **De-identification & Redaction:** Even when tweets are posted publicly, aggregating and labeling identifiable accounts with psychiatric diagnoses without informed consent introduces risks of stigma, re-identification, and harassment.
* **Anonymization Approach in this Repository:**
  1. All personal identifiers (`user_screen_name`, `user_id`, profile URLs, and bio text) have been removed from public artifacts.
  2. Public demonstration datasets use masked synthetic identifiers (e.g., `user_001`, `user_002`).
  3. Analysis code is decoupled from raw personal data and operates on aggregated numerical and categorical features.

---

## 3. Reproduction & Academic Inquiries

Researchers seeking access to anonymized feature tables or validation scripts for replication purposes are invited to consult the technical report located at [`report/Analyzing_Twitter_Follower_Homogeneity.pdf`](../report/Analyzing_Twitter_Follower_Homogeneity.pdf) or contact the author.
