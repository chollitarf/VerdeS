# VerdeS

## Overview

**VerdeS** is a decentralized **Carbon Credit Trading Platform** built on the Stacks blockchain. It enables transparent management of carbon offset projects — from registration and verification to credit issuance, trading, and retirement. By leveraging smart contract automation, VerdeS ensures traceability, verifiability, and accountability in the carbon credit ecosystem.

---

## Key Features

### 1. Project Registration

* Organizations can register **carbon offset projects** with details such as name, type, location, duration, and registry information.
* Supported project types include:

  * Renewable Energy
  * Reforestation
  * Methane Capture
  * Energy Efficiency
  * Carbon Capture

### 2. Project Verification

* **Authorized verifiers** confirm project legitimacy and issue verified carbon credits.
* Each verification includes:

  * Verification report URL
  * Methodology
  * Issued credits
  * Verification period
* Verified projects move from **“pending”** to **“active”** status.

### 3. Credit Issuance and Batching

* Project owners can create **credit batches** that represent verified carbon credits available for sale.
* Each batch contains:

  * Vintage year
  * Quantity
  * Price per unit
  * Status (available, sold, or retired)

### 4. Credit Trading

* Buyers can purchase carbon credits directly using STX.
* Funds are transferred automatically to the project owner.
* Purchased credits are stored in the buyer’s **credit balance**, tied to project ID and vintage year.

### 5. Credit Retirement

* Users can **retire carbon credits** to offset their emissions.
* Each retirement generates an immutable record containing:

  * Retirement reason
  * Quantity retired
  * Beneficiary (optional)
  * Timestamp
* Admins can issue a **retirement certificate** URL to confirm the offset officially.

### 6. Authorized Verifier Management

* Admins can register and manage authorized verifiers with:

  * Name
  * Credentials
  * Authorization timestamp
  * Status (active/inactive)

### 7. Token and Trait Definition

* Includes a local implementation of the **SIP-010 Fungible Token Trait** to facilitate potential integration with on-chain carbon credit tokens.

---

## Core Data Structures

| Map / Variable                                           | Description                                                 |
| -------------------------------------------------------- | ----------------------------------------------------------- |
| `registered-projects`                                    | Stores metadata for all carbon offset projects.             |
| `verification-records`                                   | Tracks verifier activity and credit issuance events.        |
| `credit-lots`                                            | Defines tradable batches of carbon credits.                 |
| `user-credit-holdings`                                   | Maintains user credit balances by project and vintage year. |
| `offset-records`                                         | Logs details of retired carbon credits.                     |
| `approved-verifiers`                                     | Records verifier identities and authorization details.      |
| `available-project-categories`                           | Lists supported project types.                              |
| `next-project-id`, `next-batch-id`, `next-retirement-id` | Track incremental IDs for new records.                      |

---

## Public Functions

### Project Management

* **`register-project(...)`**
  Registers a new project with validation for type, timeline, and metadata.

* **`verify-project(...)`**
  Allows authorized verifiers to confirm project validity and issue carbon credits.

* **`authorize-verifier(...)`**
  Admin-only function to approve a new verifier.

### Credit Management

* **`create-credit-batch(...)`**
  Allows verified project owners to list carbon credits for sale.

* **`buy-carbon-credits(...)`**
  Enables buyers to purchase credits directly using STX.

* **`retire-credits(...)`**
  Retires owned credits to record an official carbon offset.

* **`transfer-credits(...)`**
  Enables peer-to-peer transfers of credits between users.

* **`generate-retirement-certificate(...)`**
  Admin-only function to attach a certificate URL to a retired batch.

---

## Read-Only Functions

| Function                                             | Description                             |
| ---------------------------------------------------- | --------------------------------------- |
| `get-project-details(project-id)`                    | Returns complete project metadata.      |
| `get-batch-details(batch-id)`                        | Retrieves details of a credit batch.    |
| `get-credit-balance(user, project-id, vintage-year)` | Returns a user’s credit balance.        |
| `get-retirement-details(retirement-id)`              | Fetches details of a retirement record. |

---

## Validation and Security

* **Admin-only actions**: Verifier authorization and certificate generation.
* **Input sanitization**: Strings and types are cast to prevent invalid data.
* **Assertions**:

  * Prevent invalid dates or zero values.
  * Ensure verifiers are authorized.
  * Restrict actions to rightful owners.
* **Traceability**: Every project, verification, and retirement is recorded immutably.

---

## Example Workflow

1. **Project Creation**
   Developer registers a project (e.g., “Solar Power in Kenya”).

2. **Verification**
   Authorized verifier reviews the project and issues credits.

3. **Credit Batch Creation**
   Project owner lists a portion of credits for sale.

4. **Trading**
   Buyers purchase credits using STX; balances update automatically.

5. **Retirement**
   Buyer retires credits to offset emissions; an immutable record is created.

6. **Certification**
   Admin issues a retirement certificate URL for public validation.

---

## Design Principles

* **Transparency:** Every credit and project status is visible on-chain.
* **Accountability:** Verification and retirement are traceable to identities.
* **Sustainability:** Supports multiple project types and future tokenization.
* **Interoperability:** SIP-010 trait allows seamless integration with fungible token systems.
