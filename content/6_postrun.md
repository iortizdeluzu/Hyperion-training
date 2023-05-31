---
title: Post-run
nav: true
---

<style>
.text {
  margin-bottom: 10px;
}
</style>

# Post-Run Operations

<div align="justify" class="text">
Once the work is finished we should move the generated data to our home directory under /dipc or to a local folder. This is done for two main reasons:</div>


1. The **scrath is not backed up**, so in case there is a problem with the filesystem, the stored data will be lost.
2. The /scratch file system is designed for performance rather than reliability. When the occupancy goes above 80% the BeeGFS filesystem shows a performance degradation that affects **all users**.

<br> <!-- Blank line -->
## Analyzing job performance with seff

<div align="justify" class="text">
SLURM provides a tool called <code>seff</code> to check the memory utilization and CPU efficiency for completed jobs. Note that for running and failed jobs, the efficiency numbers reported by seff are not reliable so please use this tool only for successfully completed jobs:</div>

```
seff <job_id>
```

