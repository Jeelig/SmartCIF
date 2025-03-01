# Smart CIF Application Specification

## 1. Overview
**Project Name:** Smart CIF  
**Purpose:** Smart CIF is an application integrated with the Channel Integration Framework (CIF) in Dynamics 365 Customer Engagement, designed to enhance agent productivity by providing real-time customer insights, call functionality, and knowledge base access within a unified interface. The app aims to streamline workflows for agents handling customer interactions, leveraging Dynamics 365 data and custom configurations.

**Status:** (Due to project constraints during the hackathon, the concept was not fully implemented, but development will continue to realize its full potential)

## 2. Key Features
### 2.1 Call Functionality
- Agents can initiate and manage calls directly from the Smart CIF interface, integrated with Dynamics 365’s telephony capabilities via CIF.
- Supports real-time call tracking and logging (in progress).

### 2.2 Contextual Information Display
- When viewing a contact or account in Dynamics 365, Smart CIF displays key information, including:
  - Open cases associated with the contact or account.
  - Customer loyalty tier (e.g., Gold, Silver, or custom levels), displayed with a customizable icon and color.
  - Loyalty tier configurations are managed via app settings and stored in the `AI_Enrichment` table for dynamic enrichment.
Agents have access to the knowledge base everytime, whether they are in a call or not

### 2.3 Knowledge Base Access
- Agents can access the Dynamics 365 knowledge base directly from Smart CIF, enabling quick retrieval of articles and solutions without leaving the interface.

### 2.4 Customization
- Admins can configure loyalty tiers, icons, and colors via a settings panel, with data stored and retrieved from the `AI_Enrichment` table.

## 3. Technical Architecture
### 3.1 Integration
- **Platform:** Built on Microsoft Dynamics 365 Customer Engagement, utilizing the Channel Integration Framework (CIF) for seamless embedding within the Dynamics 365 interface.
- **Hosting:** Deployed on Microsoft Azure, leveraging Dynamics 365’s cloud infrastructure for scalability and reliability.
- **Authentication:** Uses Dynamics 365 security and OAuth 2.0 for secure access by agents.

### 3.2 Data Model
The core data for Smart CIF’s enrichment features is stored in the `AI_Enrichment` table in Dynamics 365. Below are the columns as provided in the table structure (custom fields only):

| **Display Name**    | **Name**               | **Data Type**         | **Managed** | **Custom** |
|---------------------|-----------------------|-----------------------|-------------|------------|
| AIEnrichment        | gba_AIEnrichmentId    | Unique Identifier     | No          | Yes        |
| color               | gba_color             | Single Line of Text   | No          | Yes        |
| Condition           | gba_Condition         | Choice                | No          | Yes        |
| Description         | gba_Description       | Single Line of Text   | No          | Yes        |
| Enrichment          | gba_Enrichment        | Single Line of Text   | No          | Yes        |
| Field               | gba_Field             | Single Line of Text   | No          | Yes        |
| icon                | gba_icon              | Single Line of Text   | No          | Yes        |
| Table               | gba_Table             | Single Line of Text   | No          | Yes        |
| Type                | gba_Type              | Choice                | No          | Yes        |
| Value               | gba_Value             | Single Line of Text   | No          | Yes        |

#### Description of Columns:
- **gba_AIEnrichmentId:** Unique identifier for each enrichment record.
- **gba_color:** Stores the color code (e.g., HEX value) for loyalty tier visualization.
- **gba_Condition:** Defines conditions for displaying enrichment (e.g., loyalty tier rules), stored as a choice field.
- **gba_Description:** Provides a description of the enrichment (e.g., “Gold Customer Tier”).
- **gba_Enrichment:** General enrichment data or metadata for the record.
- **gba_Field:** Specifies the Dynamics 365 field on which enrichment is made (e.g., if number of employee is more than 5000 then is gold customer).
- **gba_icon:** Stores the icon (material icon) name for visual representation of loyalty tiers.
- **gba_Table:** Indicates the Dynamics 365 table (e.g., Account, Contact) associated with the enrichment.
- **gba_Type:** Defines the type of enrichment (e.g., loyalty, case status), stored as a choice field.
- **gba_Value:** Holds the value of the enrichment (e.g., “Gold,” “Open Case”).

### 3.3 UI/UX
- **Interface:** Embeds as a panel within Dynamics 365 via CIF, with a clean, intuitive design for quick access to calls, customer data, and the knowledge base.
- **Customization:** Supports admin-configurable settings for loyalty tiers, icons, and colors, displayed dynamically using data from `AI_Enrichment`.

## 4. Development Plan
### 4.1 Current State
- The concept was partially developed during the hackathon but not fully implemented due to project constraints.
- Core features (e.g., call functionality, basic data display) are in progress, with the `AI_Enrichment` table structure defined.

### 4.2 Future Steps
- Complete integration of call functionality with CIF and Dynamics 365 telephony.
- Fully implement loyalty tier visualization using the `AI_Enrichment` table for dynamic color and icon display.
- Add knowledge base access and optimize performance for scalability.
- Conduct testing for performance, security, and user experience across different agent roles and volumes.

## 5. Business Value
- **Agent Productivity:** Reduces time spent switching between systems by providing all necessary tools in one interface.
- **Customer Satisfaction:** Enhances agent ability to deliver personalized, informed responses based on real-time data.
- **Scalability:** Supports enterprise-wide deployment with minimal customization, leveraging Dynamics 365’s infrastructure.

## 6. Dependencies
- Microsoft Dynamics 365 Customer Engagement (latest version).
- Channel Integration Framework (CIF) for embedding and telephony integration.
- Microsoft Azure for hosting, scaling, and caching.
- Dynamics 365 API access for data retrieval and updates.
- Twilio SDK

## 7. Risks and Mitigation
- **API Rate Limits:** Monitor and optimize Dynamics 365 API calls using caching and batch processing.
- **Incomplete Implementation:** Prioritize core features (e.g., call handling, loyalty display) for initial release, with iterative updates for knowledge base and advanced customizations.
- **Scalability Issues:** Use Azure’s monitoring tools to identify bottlenecks and scale resources dynamically.

