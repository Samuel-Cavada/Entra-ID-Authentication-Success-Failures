<p align="center">
  <a href="https://github.com/Samuel-Cavada" target="_blank">
    <img src="https://img.shields.io/badge/Back_to_Main_Page-000000?style=for-the-badge&logo=github&logoColor=white" alt="Back to Main Page"/>
  </a>
</p>

<h1 align="center">Entra ID Authentication Success / Failures</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Azure%20Sentinel-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Cloud Platform" />
  <img src="https://img.shields.io/badge/OS-N/A-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="OS" />
  <img src="https://img.shields.io/badge/Tool-Azure%20Workbooks-00B388?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Tool" />
  <img src="https://img.shields.io/badge/Tool-PowerShell-2C5EA8?style=for-the-badge&logo=powershell&logoColor=white" alt="Tool" />
  <img src="https://img.shields.io/badge/Focus-Authentication%20Monitoring-orange?style=for-the-badge" alt="Focus Area" />
</p>

---

## 📌 Project Objective
> Create interactive world map visualizations in Azure Sentinel Workbooks to monitor successful and failed authentication attempts in Entra ID (Azure AD). This project focuses on geolocation-based analysis for understanding login patterns and suspicious access activity.

---

## 🧰 Tools & Technologies
- **Platform:** Azure Sentinel
- **OS:** N/A
- **Tools:** Azure Workbooks, Log Analytics, PowerShell
- **Languages/Scripts:** KQL

---

## 🧠 Skills Gained / Focus Areas
- Built geolocation-based dashboards for authentication logs
- Differentiated between success and failure events
- Used KQL to filter and summarize by source IP and country
- Created custom visualizations to aid security monitoring

---

## 🧪 Environment Setup
> Logged into Azure Portal, accessed Microsoft Sentinel, and opened the **Workbooks** section under **Threat Management**. Selected data from SignInLogs to visualize user login success and failures based on IP origin.

![Environment Setup](assets/images/setup.jpg)

---

## 🛠️ Walkthrough
1. [Step 1: Access Workbook Tools](#step-1-access-workbook-tools)
2. [Step 2: Configure Success & Failure Queries](#step-2-configure-success--failure-queries)
3. [Step 3: Visualize by Geography](#step-3-visualize-by-geography)

---

### ✅ Step 1: Access Workbook Tools
> - Opened Azure Sentinel  
> - Went to **Threat Management** → **Workbooks**  
> - Clicked **Add Workbook** to begin designing the visualization  
> - Selected **Log Analytics** as the data source

![Step 1](assets/images/step1.jpg)

---

### ✅ Step 2: Configure Success & Failure Queries
> Sample KQL for authentication **successes**:
```kql
SigninLogs
| where ResultType == 0 and TimeGenerated > ago(1d)
| summarize count() by tostring(LocationDetails["countryOrRegion"]), IPAddress
```

> Sample KQL for authentication **failures**:
```kql
SigninLogs
| where ResultType != 0 and TimeGenerated > ago(1d)
| summarize count() by tostring(LocationDetails["countryOrRegion"]), IPAddress
```

> Adjusted queries for:
> - Filtering by user role or application
> - Custom time ranges
> - Aggregating by source IP, device, and region

![Step 2](assets/images/step2.jpg)

---

### ✅ Step 3: Visualize by Geography
> - Used the **Map** visualization in Workbooks  
> - Mapped IP addresses to geographic regions using `LocationDetails`  
> - Created two views: one for successful logins, one for failures  
> - Allowed filtering by user, time, and country

![Step 3](assets/images/step3.jpg)

---

## 📝 Outcomes and Lessons Learned
- **Technical Insight:** Login success and failure trends offer visibility into both user behavior and potential brute-force attacks.
- **Configuration Skills:** Created geolocation dashboards using Log Analytics and KQL.
- **Troubleshooting:** Refined log queries to handle null values and enhance map accuracy.
- **Takeaway:** Visualizing login data enhances understanding of authentication risks and user distribution globally.

---

## 📎 References
- [SignInLogs Reference](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/tables/signinlogs)
- [Azure Workbooks Documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/workbooks-overview)
- [KQL for Log Analytics](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)
