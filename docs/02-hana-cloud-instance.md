# SAP HANA Cloud – Instance Provisioning

## 1. Overview

This document describes the subscription, authorization and provisioning
process for SAP HANA Cloud within the SAP Business Technology Platform
(BTP) Trial environment.

The objective is to provision a SAP HANA Database instance and establish
a cloud-based environment for database administration, SQL development
and data modeling.

## 2. Environment and Prerequisites

The following environment was used:

| Component | Configuration |
|---|---|
| Platform | SAP Business Technology Platform |
| Environment | SAP BTP Trial |
| Cloud Provider | Amazon Web Services (AWS) |
| Region | US East (Virginia) |
| Subaccount | trial |
| SAP HANA Service | SAP HANA Cloud |
| Instance Type | SAP HANA Database |
| Service Tier | Free Tier |

Before provisioning the instance, the required service entitlements
and permissions were checked in the SAP BTP Cockpit.

## 3. Entitlement Verification

The available entitlements were reviewed under the subaccount's
Entitlements section.

### 3.1 SAP HANA Cloud

The following service plans were identified:

- `tools` (Application)
- `relational-data-lake-free`
- `hana-free`
- `hana-cloud-connection-free`

### 3.2 SAP HANA Schemas & HDI Containers

The following plans were also available:

- `hdi-shared`
- `schema`
- `sbss`
- `securestore`

These entitlements provide the service plans required for the
SAP HANA Cloud tools and related database services.

**Evidence:** `screenshots/02-hana-cloud-instance/02-hana-cloud-entitlements.png`

## 4. Service Subscription

The SAP HANA Cloud service was located through the SAP BTP
subaccount Service Marketplace.

The service was selected and its application plan was reviewed.
The `tools` application plan was available.

The subscription was then created and verified under
Services > Instances and Subscriptions.

The SAP HANA Cloud application appeared with the subscription
status `Subscribed`.

**Evidence:**
- `screenshots/02-hana-cloud-instance/03-service-marketplace.png`
- `screenshots/02-hana-cloud-instance/04-sap-hana-cloud-subscription.png`

## 5. Authorization and Role Assignment

### 5.1 Initial Access Issue

When SAP HANA Cloud Central was accessed for the first time,
the application displayed a `Not authorized` message.

The message indicated that the selected identity provider
was missing the required SAP HANA Cloud roles.

This demonstrated that service subscription alone was not
sufficient to grant access to the administration application.

### 5.2 Role Collection Assignment

The user was located under Security > Users in the SAP BTP Cockpit.

The following role collections were assigned:

- `Subaccount Administrator`
- `SAP HANA Cloud Administrator`

The SAP HANA Cloud Administrator role collection provides
permissions to create, update and delete SAP HANA Cloud
service instances.

After assignment, the role collections were visible in
the user's authorization details.

**Evidence:**
- `screenshots/02-hana-cloud-instance/05-sap-hana-cloud-role-assignment.png`
- `screenshots/02-hana-cloud-instance/06-sap-hana-cloud-roles-assigned.png`

### 5.3 Access Verification

SAP HANA Cloud Central was accessed again after the role
assignment process.

The application opened successfully and displayed the
Instances administration page.

At that point, no database instances were listed.

**Evidence:**
`screenshots/02-hana-cloud-instance/07-sap-hana-cloud-central-access.png`

## 6. SAP HANA Database Instance Provisioning

The Create Instance workflow was started from SAP HANA
Cloud Central.

### 6.1 Instance Type

The following options were selected:

- Instance configuration: Configure manually
- Instance type: SAP HANA Database

The Data Lake option was not selected as the primary
instance type.

**Evidence:**
`screenshots/02-hana-cloud-instance/08-hana-instance-type-configuration.png`

### 6.2 General Configuration

The general instance parameters were configured as follows:

| Parameter | Value |
|---|---|
| Instance Name | `hana-learning-lab` |
| Description | Personal SAP HANA Cloud learning environment for database administration, SQL development and data modeling |
| Administrator | `DBADMIN` |
| Runtime Environment | Other Environments |

An administrator password was configured during this step.
For security reasons, credentials are not included in this
documentation or stored in the repository.

**Evidence:**
`screenshots/02-hana-cloud-instance/09-hana-instance-general-configuration.png`

### 6.3 Size and Availability

The Free Tier configuration provided the following resources:

| Resource | Configuration |
|---|---|
| Memory | 16 GB |
| Compute | 1 vCPU |
| Storage | 80 GB |
| Nodes | 1 Coordinator |
| Replicas | 0 |
| Performance Class | Memory |
| Compute-Memory Ratio | 1:16 |

The instance size was fixed by the Free Tier service plan.

Automatic storage upsizing and additional replicas were
not available under this tier.

**Evidence:**
`screenshots/02-hana-cloud-instance/10-hana-instance-size-availability.png`

### 6.4 Network Connections

The following connection policy was selected:

`Only IP addresses from Cloud Foundry in this BTP region`

Other available options included allowing all IP addresses
or specifying individual IP addresses and ranges.

The Cloud Connector (Dedicated) option remained disabled.

This configuration was retained for the learning environment.

**Evidence:**
`screenshots/02-hana-cloud-instance/11-hana-instance-connections.png`

### 6.5 Advanced Settings

The following database version was selected:

- Version: `2026.28 (QRC 3/2026)`
- Maintenance until: April 15, 2027

No additional features were enabled.

No Cloud Foundry instance mapping was configured during
the provisioning process.

**Evidence:**
`screenshots/02-hana-cloud-instance/12-hana-instance-advanced.png`

### 6.6 Data Lake Configuration

The optional Data Lake creation setting was left disabled.

The configuration therefore focused on provisioning
the SAP HANA Database instance without an additional
Data Lake instance.

**Evidence:**
`screenshots/02-hana-cloud-instance/13-hana-instance-data-lake.png`

## 7. Final Configuration Review

Before submitting the provisioning request, the final
configuration was reviewed.

The instance summary showed:

- Instance name: `hana-learning-lab`
- Instance type: SAP HANA Database
- Memory: 16 GB
- Compute: 1 vCPU
- Storage: 80 GB
- Runtime environment: Other Environments
- Cloud Connector: Disabled
- Data Lake: Not selected

The configuration was reviewed before selecting Create Instance.

**Evidence:**
`screenshots/02-hana-cloud-instance/14-Create-hana-instance-data-lake.png`

## 8. Deployment Status

The instance appeared in SAP HANA Cloud Central with the
name `hana-learning-lab`.

The initial status displayed was `Starting`.

This confirms that the provisioning process had been initiated.
A successful transition to the running state and subsequent
database connectivity checks must be documented separately.

The instance is therefore not considered fully operational
at this stage of the documentation.

## 9. Security Considerations

The following security practices were applied:

- Administrative access was assigned through role collections.
- The DBADMIN password was not included in the repository.
- Network access was restricted to the selected Cloud Foundry
  IP address policy.
- The Cloud Connector remained disabled.
- Screenshots and documentation should not expose passwords,
  access tokens or other authentication secrets.

## 10. Results and Next Steps

The SAP HANA Cloud service was subscribed successfully,
the required administrative role collections were assigned
and the database instance provisioning workflow was completed.

The initial deployment status was `Starting`.

The next steps are:

1. Verify that the instance reaches the running state.
2. Access the instance through SAP HANA Cloud Central.
3. Verify database connectivity.
4. Explore the SQL Console.
5. Start working with schemas and database objects.
6. Document the practical SQL exercises.

## 11. References

- [SAP Business Technology Platform](https://www.sap.com/products/technology-platform.html)
- [SAP HANA Cloud Documentation](https://help.sap.com/docs/hana-cloud)
- [SAP BTP Cockpit Documentation](https://help.sap.com/docs/btp/sap-business-technology-platform)

---

**Project:** SAP BTP Learning Lab  
**Document:** SAP HANA Cloud Instance Provisioning  
**Status:** Provisioning initiated; operational verification pending.
