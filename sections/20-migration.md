# **Migration Services**

| Service | Migrates | Key Facts |
| ----- | ----- | ----- |
| AWS DMS (Database Migration Service) | Databases (homogeneous or heterogeneous) | Minimal downtime; continuous replication (CDC); Schema Conversion Tool (SCT) for heterogeneous migrations (e.g., Oracle → PostgreSQL) |
| AWS SMS (Server Migration Service) | On-prem virtual machines | Lift-and-shift VMs; incremental replication; Agentless; now superseded by Application Migration Service |
| AWS Application Migration Service (MGN) | Physical, virtual, cloud servers | Continuous block-level replication; cutover with minimal downtime; replaces SMS |
| AWS Snowball Edge (Storage Optimized) | Large data volumes (TBs to PBs) offline | 80 TB usable storage; petabyte-scale data transfer; for areas with limited bandwidth |
| AWS Snowmobile | Exabyte-scale data transfer | A 45-foot shipping container truck; for \> 10 PB migrations |
| AWS DataSync | File/NFS/SMB data to AWS (online) | Scheduled sync; on-prem NFS/SMB/HDFS → S3/EFS/FSx; agent-based; faster than cp over DX |
| AWS Transfer Family | SFTP/FTP/FTPS to/from S3 or EFS | Managed SFTP server endpoint backed by S3; no protocol change needed for clients |

| 💡 TIP: Snowball decision: \< 10 PB → Snowball Edge (multiple units). \> 10 PB → Snowmobile. Rule of thumb: if it would take \> 1 week to transfer over your network, use Snowball. |
| :---- |

---

[< Core Architectural Patterns for SAA](19-architectural-patterns.md) | [Back to README](../README.md) | [Analytics Services >](21-analytics.md)
