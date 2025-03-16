# **Azure Cost Estimation Report**

This is a cost estimate for hosting a **2-Tier Application** on **Microsoft Azure**,
using the **Azure Pricing Calculator**. Prices are estimated as of **March 15, 2025, 10:55 PM UTC**, 
and the costs are in **USD** for the **Canada Central** region.

---
## **Architecture Overview**

This cloud architecture will have:

**Frontend**: 1 Virtual Machine (**B2s**, 2 vCPUs, 4GB RAM, 64GB storage)<p></p>
**Backend**: 1 Virtual Machine (**D2s_v3**, 2 vCPUs, 8GB RAM, 128GB storage)<p></p>
**Database**: Azure **SQL Database** (Standard **S0**, 10 DTUs, 250GB storage)<p></p>
**Networking**: **200 GB outbound data transfer** via Microsoft Global Network<p></p>

---
## **Frontend VM Configuration**
| Parameter       | Value |
|----------------|------------------------------------------------|
| **Service Type** | Virtual Machines |
| **Instance Type** | B2s (2 Cores, 4 GB RAM) |
| **Billing** | 730 Hours (Pay as you go) |
| **OS** | Windows (License included) |
| **Disk Type** | Managed Disk - **S6 (64GB)** |
| **Network** | 5 GB outbound data transfer (Inter Region) |

---
## **Backend VM Configuration**
| Parameter       | Value |
|----------------|------------------------------------------------|
| **Service Type** | Virtual Machines |
| **Instance Type** | D2s_v3 (2 vCPUs, 8GB RAM) |
| **Billing** | 730 Hours (Pay as you go) |
| **OS** | Windows (License included) |
| **Disk Type** | Managed Disk - **S10 (128GB)** |
| **Network** | 5 GB outbound data transfer (Inter Region) |

---
## **Networking (Bandwidth)**
| Parameter       | Value |
|----------------|------------------------------------------------|
| **Service Type** | Bandwidth |
| **Description** | Internet egress, **200 GB outbound data transfer** |
| **Routed via** | Microsoft Global Network

## **Database Configuration**
| Parameter       | Value |
|----------------|------------------------------------------------|
| **Service Type** | Azure SQL Database |
| **Purchase Model** | DTU-based |
| **Tier** | Standard (S0) |
| **DTUs** | 10 DTUs |
| **Storage** | 250 GB |
| **Backup Storage** | LRS Backup Storage Redundancy |

---
## **Cost Breakdown**

| Service Category | Service Type | Estimated Monthly Cost (USD) |
|-----------------|-------------|------------------------------|
| Compute        | Frontend VM (B2s)  | **$43.02** |
| Compute        | Backend VM (D2s v3)  | **$154.67** |
| Networking     | Bandwidth (200 GB) | **$8.70** |
| Databases      | Azure SQL Database | **$16.18** |
| Support       | Basic Support (Included) | **$0.00** |
| **Total Estimated Monthly Cost** |  | **$222.57** |

---

##  **Additional Information**

- **Licensing Program:** Microsoft Customer Agreement (MCA)  
- **Billing Account/Profile:** Not specified  
- **Estimated Upfront Cost:** **$0.00**  
- **Total Estimated Monthly Cost:** **$222.57**  

---

##  **Disclaimer**
All costs are in **USD** and are an **estimate, not a quote**.
For the most current and accurate costs, please utilize the **[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/)**.

---

## **Summary**

The estimated **monthly cost** to operate this **2-tier application** in **Canada Central** is **$222.57**.
This setup provides a fault-tolerant cloud infrastructure with a scalable database and a secure network architecture.


