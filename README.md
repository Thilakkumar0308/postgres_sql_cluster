# PostgreSQL Cluster Metrics

## 1. Metrics (Numeric Only)

| **Metric Name** | **Description** |
|----------------|----------------|
| Active Connections | Number of currently active database connections |
| Active Replication Slots | Count of active replication slots |
| Archive Ready Files Count | WAL files ready to be archived |
| Archive Status Failed | Number of failed archive attempts |
| Archive Status Success | Number of successful archive operations |
| Available Connections | Remaining available connection slots |
| Buffers Allocated | Number of allocated shared buffers |
| Buffers Backend Direct Writes | Direct writes performed by backend processes |
| Buffers Checkpoint | Buffers written during checkpoints |
| Buffers Clean | Buffers cleaned by background writer |
| Checkpoint Sync | Time spent syncing checkpoint data |
| Checkpoint Write | Time spent writing checkpoint data |
| Checkpoints Requested | Number of manually triggered checkpoints |
| Checkpoints Timed | Number of scheduled checkpoints |
| Conflicts Buffer Pin | Conflicts due to buffer pin issues |
| Conflicts Deadlock | Deadlock-related conflicts |
| Conflicts Lock | Conflicts due to lock issues |
| Conflicts Snapshot | Conflicts due to snapshot issues |
| Conflicts Tablespace | Conflicts due to tablespace issues |
| Connection Utilization Percent | Percentage of used connections |
| Current WAL LSN | Current WAL log sequence number |
| Flush Lag | Delay in flushing WAL to disk |
| Inactive Replication Slots | Count of inactive replication slots |
| Last Received LSN | Last WAL location received by replica |
| Last Replayed LSN | Last WAL location replayed on replica |
| Logical Slots | Number of logical replication slots |
| Maxwritten Clean | Times background writer stopped due to limits |
| Oldest Running Transaction Age | Age of the oldest active transaction |
| Physical Slots | Number of physical replication slots |
| Receive Apply Lag | Delay between receiving and applying WAL |
| Recovery Conflicts Total | Total recovery conflicts on replica |
| Replay Lag | Delay in WAL replay |
| Replay Lag Time | Time delay in WAL replay |
| Replica Count | Number of connected replicas |
| Replication Lag | Delay between primary and replica |
| Replication Slot Count | Total replication slots |
| Slot Lag | Replication slot delay |
| Timeline ID | Current WAL timeline identifier |
| WAL Files Count | Number of WAL files present |
| WAL Flush LSN | WAL position flushed to disk |
| WAL Insert LSN | WAL position inserted |
| WAL Total Size | Total size of WAL files |
| Write Lag | Delay in writing WAL |

---

## 2. Configuration (Static / Limits)

| **Metric Name** | **Description** |
|----------------|----------------|
| Max Connections | Maximum allowed database connections |
| Superuser Reserved Connections | Connections reserved for superusers |

---

## 3. Textual Attributes (Status / Info)

| **Metric Name** | **Description** |
|----------------|----------------|
| Cluster Name | Name of the PostgreSQL cluster |
| Cluster Status | Current health/status of the cluster |
| Is In Recovery | Whether the node is in recovery mode |
| Last Archived WAL File | Last successfully archived WAL file |
| Node Role | Role of node (Primary/Replica) |
| PostgreSQL Version | Installed PostgreSQL version |
| Replication State | Current replication status |
| Server PID | Process ID of PostgreSQL server |
| Server Uptime | Time since server started |
| Sync State | Replication sync mode (sync/async) |
| WAL Receiver Status | Status of WAL receiver process |
