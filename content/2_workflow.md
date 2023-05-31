---
title: Workflow
nav: true
---

# Workflow

<div align="justify">
The typical workflow of a researcher using SLURM in an HPC environment involves several steps:
</div>
<br> <!-- Blank line -->

1. **Connect to the System**: Using Secure Shell (SSH), you connect to the login node of the HPC cluster.

2. **Prepare Your Work**: This might include copying input files, writing scripts, or compiling programs.

3. **Job Submission**: You write a batch script for SLURM that outlines the requirements and commands for your job, and submit this script to the scheduler.

4. **Monitor Your Job**: You can keep track of your job's progress using several SLURM commands.

5. **Transfer Results**: Once your job is completed, you can copy your output files from the compute node back to your local system.

<br> <!-- Blank line -->

<div align="justify">
In the following sections, we will delve into each of these steps, starting with a detailed walkthrough of a simple example.</div>

