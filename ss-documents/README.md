---
description: SS-IdentityCard documentation
---

# SS-Documents

<figure><img src="../.gitbook/assets/COVER 1.png" alt=""><figcaption></figcaption></figure>

**Overview**



**SS-Documents** is a powerful and fully customizable **official documents system** for RedM, built as an **addon for SS-IdentityCard**. It allows players to create, sign, and share unlimited legal documents such as certificates, licenses, contracts, statements, and more—fully integrated into immersive roleplay.

With Western-style UI, handwriting simulation, job-based permissions, and full in-game usage, SS-Documents enhances realism for both legal and criminal scenarios in any RP server.

> **Requires SS-IdentityCard.**



### Custom Document Creation System

* Players can create unlimited **official and customized documents**.
* Each document includes:
* Title, subtitle, and official information headers.
* Fillable fields: input boxes, dates, and text areas.
* Once completed, the document is **signed and saved** on the server.

***

* #### Job-Based Access & Permissions
  * Documents are **restricted by job roles**, using the `AllowedDocs` configuration.
  * Examples:
    * Only **Governor** jobs can issue **Pardon Certificates** or **Political Affiliation forms**.
      * **Police roles** can issue **Firearm Licenses**.
      * **Mayors** can create **Marriage Certificates**, **Employment Contracts**, and **Divorce Agreements**.

***

* #### Predefined Categories & Documents
  * Built-in document categories, each with custom access:
    * **Public** – Statements, witness reports, denunciations.
      * **Police** – Firearm licenses.
      * **Mayor** – Sales declarations, debts, employment contracts, marriage, divorce.
      * **Marshal** – Search warrants.
      * **Governor** – Political certificates, pardon documents.

***

* #### Immersive UI & Features
  * Western-style **paper UI** with handwritten-like appearance.
  * Fully translated document categories and descriptions.
  * In-game **menu navigation**, aligned left or right (`Config.Align`).
  * Option to **show or view** documents to/from nearby players.

***

* #### Fully Configurable
  * Easily customize:
    * Document titles, subtitles, content structure.
      * Access permissions per job.
      * Category names, descriptions, and language.
      * Uses a configurable item (e.g., `cocoa`) as paper to start a new document.
      * Server-side saving with feedback on success.

