# Plugin for PostgreSQL Cluster Monitoring

PostgreSQL Cluster monitoring plugin provides **cluster-level visibility** including replication health, WAL activity, checkpoints, connection usage, and recovery conflicts — all in one place.

This plugin is designed to monitor **Primary and Standby nodes together as a cluster**, giving deep insights into replication status and overall system performance across your entire PostgreSQL setup.

Learn more: [https://www.site24x7.com/plugins/postgres-monitoring.html](https://www.site24x7.com/plugins/postgres-monitoring.html)

---

## Quick Installation

If you're using Linux servers, use the plugin installer that checks prerequisites and sets up the plugin automatically using a bash script. You don't need to manually configure the plugin if you use the installer.

Execute the command below in your terminal and follow the on-screen instructions:

```bash
wget https://raw.githubusercontent.com/site24x7/plugins/master/postgres_cluster/installer/Site24x7PostgresClusterPluginInstaller.sh && sudo bash Site24x7PostgresClusterPluginInstaller.sh
```

---

## Prerequisites

- Download and install the latest version of the [Site24x7 agent](https://www.site24x7.com/app/client#/admin/inventory/add-monitor) on the server where you plan to run the plugin.
- Python 3 or higher.
- Install the required Python library:

```bash
pip3 install psycopg2-binary
```

---

## Plugin Installation

### Step 1 — Create the plugin directory

```bash
mkdir postgres_cluster
cd postgres_cluster/
```

### Step 2 — Download the plugin files

```bash
wget https://raw.githubusercontent.com/site24x7/plugins/master/postgres_cluster/postgres_cluster.py
wget https://raw.githubusercontent.com/site24x7/plugins/master/postgres_cluster/postgres_cluster.cfg
```

### Step 3 — Grant the required database permissions

Ensure the monitoring user has the necessary roles. For example, to grant permissions to the user `admin`:

```sql
GRANT pg_read_all_settings TO admin;
GRANT pg_monitor TO admin;
```

### Step 4 — Configure the plugin

Edit `postgres_cluster.cfg` and provide your PostgreSQL cluster details:

```ini
[global_configurations]
use_agent_python = 1

[pg_primary]
host = 192.168.56.1
port = 5433
username = admin
password = admin123
cluster_name = pg_cluster_01

[pg_replica]
host = 192.168.56.1
port = 5434
username = admin
password = admin123
cluster_name = pg_cluster_01
```

### Step 5 — Test the plugin

Run the following command to verify the plugin produces valid output before deployment:

```bash
python3 postgres_cluster.py --host "192.168.56.1" --port "5433" --username "admin" --password "admin123" --cluster_name "pg_cluster_01"
```

---

## Deploying the Plugin

### Linux

Follow [this guide](https://support.site24x7.com/portal/en/kb/articles/updating-python-path-in-a-plugin-script-for-linux-servers) to update the Python path in the plugin script, then move the directory to the Site24x7 agent plugin folder:

```bash
mv postgres_cluster /opt/site24x7/monagent/plugins/
```

### Windows

Since this is a Python plugin, follow [these steps](https://support.site24x7.com/portal/en/kb/articles/run-python-plugin-scripts-in-windows-servers) to configure Python plugins on Windows. Then move the folder to the Site24x7 Windows agent plugin directory:

```
C:\Program Files (x86)\Site24x7\WinAgent\monitoring\Plugins\
```

The agent will automatically execute the plugin within five minutes. You can view the monitor under:

**Site24x7 → Plugins → Plugin Integrations**

---

## PostgreSQL Cluster Metrics

### PostgreSQL Cluster Performance Metrics

| **Metric Name** | **Description** |
|---|---|
| Active Connections | The number of client connections that are currently active and executing queries on the database. |
| Active Replication Slots | The total number of replication slots that are currently active and being consumed by a replica. |
| Archive Ready Files Count | The number of WAL segment files that have been generated and are waiting to be archived. |
| Archive Status Failed | The total number of WAL archiving attempts that have failed since the server started. |
| Archive Status Success | The total number of WAL files that have been successfully archived since the server started. |
| Available Connections | The number of remaining connection slots available for new client connections. |
| Buffers Allocated | The total number of shared memory buffers that have been allocated by the PostgreSQL server. |
| Buffers Backend Direct Writes | The number of buffers written directly to disk by backend processes, bypassing the shared buffer pool. |
| Buffers Checkpoint | The total number of buffers written to disk during checkpoint operations. |
| Buffers Clean | The total number of buffers written to disk by the background writer outside of checkpoint operations. |
| Checkpoint Sync | The total time spent synchronizing files to disk during checkpoint operations, in milliseconds. |
| Checkpoint Write | The total time spent writing dirty buffers to disk during checkpoint operations, in milliseconds. |
| Checkpoints Requested | The total number of checkpoints that were triggered manually or due to WAL size limits. |
| Checkpoints Timed | The total number of checkpoints that occurred on their scheduled interval as defined by `checkpoint_timeout`. |
| Conflicts Buffer Pin | The number of queries cancelled on the standby due to a conflict with a buffer pin held by another process. |
| Conflicts Deadlock | The number of queries cancelled on the standby due to deadlock conflicts during recovery. |
| Conflicts Lock | The number of queries cancelled on the standby due to lock conflicts with the recovery process. |
| Conflicts Snapshot | The number of queries cancelled on the standby due to snapshot conflicts, where the required row version was removed. |
| Conflicts Tablespace | The number of queries cancelled on the standby due to a tablespace being dropped on the primary during recovery. |
| Connection Utilization Percent | The percentage of the maximum allowed connections that are currently in use, calculated as (Active Connections / Max Connections) × 100. |
| Current WAL LSN | The current write-ahead log sequence number (LSN) indicating the latest position written to WAL on the primary. |
| Flush Lag | The time elapsed between WAL being written on the primary and the replica confirming it has been flushed to disk. |
| Inactive Replication Slots | The total number of replication slots that exist but are not currently being consumed by any replica. |
| Last Received LSN | The latest WAL log sequence number that the replica has received from the primary. |
| Last Replayed LSN | The latest WAL log sequence number that has been successfully applied (replayed) on the replica. |
| Logical Slots | The total number of logical replication slots configured on the PostgreSQL instance. |
| Maxwritten Clean | The number of times the background writer stopped its cleaning scan because it had written too many buffers, as controlled by `bgwriter_lru_maxpages`. |
| Oldest Running Transaction Age | The age in transactions of the oldest currently active transaction, which affects how far back VACUUM must retain dead row versions. |
| Physical Slots | The total number of physical replication slots configured on the PostgreSQL instance. |
| Receive Apply Lag | The time elapsed between WAL being received by the replica and being fully applied to the standby database. |
| Recovery Conflicts Total | The total number of queries that have been cancelled on the standby due to conflicts arising during WAL recovery. |
| Replay Lag | The time elapsed between WAL being written on the primary and the replica finishing replaying it to the standby database. |
| Replay Lag Time | The total cumulative time delay in replaying WAL on the standby, measured from when it was generated on the primary. |
| Replica Count | The total number of replica nodes currently connected to and streaming WAL from the primary. |
| Replication Lag | The total delay between the primary writing WAL and the replica applying it, indicating how far behind the replica is. |
| Replication Slot Count | The total number of replication slots present on the PostgreSQL instance, including both active and inactive slots. |
| Slot Lag | The amount of WAL data (in bytes) that a replication slot has retained on disk but not yet delivered to its consumer. |
| Timeline ID | The current WAL timeline identifier, which increments each time a standby is promoted to primary. |
| WAL Files Count | The total number of WAL segment files currently present in the `pg_wal` directory. |
| WAL Flush LSN | The WAL log sequence number up to which data has been flushed to durable storage on disk. |
| WAL Insert LSN | The WAL log sequence number up to which data has been inserted into the WAL buffer in memory. |
| WAL Total Size | The total disk space consumed by all WAL segment files currently stored in the `pg_wal` directory. |
| Write Lag | The time elapsed between WAL being written on the primary and the replica confirming it has been written (but not yet flushed) to its WAL file. |

---

### PostgreSQL Cluster Configuration Metrics

| **Metric Name** | **Description** |
|---|---|
| Max Connections | The maximum number of concurrent client connections allowed to the PostgreSQL server, as set by the `max_connections` configuration parameter. |
| Superuser Reserved Connections | The number of connection slots reserved exclusively for superuser access, as configured by `superuser_reserved_connections`, ensuring administrators can always connect even when the server is at capacity. |

---

### Cluster Status and Node Information

| **Metric Name** | **Description** |
|---|---|
| Cluster Name | The name assigned to the PostgreSQL cluster, used to identify and group the primary and replica nodes being monitored. |
| Cluster Status | The current overall health status of the cluster, reflecting whether replication and node connectivity are operating normally. |
| Is In Recovery | Indicates whether the current node is operating in recovery mode, which is true for standby/replica nodes that are replaying WAL from the primary. |
| Last Archived WAL File | The name of the most recent WAL segment file that was successfully archived by the `archive_command`. |
| Node Role | The role of the monitored node within the cluster, either Primary (accepting writes) or Replica (read-only standby). |
| PostgreSQL Version | The full version string of the PostgreSQL server software currently installed and running on the node. |
| Replication State | The current state of the replication stream, such as `streaming`, `catchup`, or `disconnected`, indicating the health of the replication connection. |
| Server PID | The operating system process ID of the PostgreSQL server's postmaster process. |
| Server Uptime | The total elapsed time since the PostgreSQL server was last started, indicating how long it has been running without a restart. |
| Sync State | The replication synchronization mode for the standby, either `sync` (the primary waits for the replica to confirm WAL receipt) or `async` (the primary does not wait). |
| WAL Receiver Status | The current status of the WAL receiver process running on the standby node, indicating whether it is actively receiving WAL data from the primary. |
