---
title: Constrains
nav: true
---

# Policies and constrains

<div align="justify">
In an HPC (High-Performance Computing) environment, imposing constraints plays a crucial role in effectively managing and optimizing job execution. These constraints collectively contribute to the overall effectiveness and fairness of job management in an HPC environment. By implementing appropriate constraints, HPC systems can enhance resource utilization, minimize job delays, and accommodate the diverse computational needs of multiple users and applications.</div>

<br> <!-- Blank line -->
<table style="text-align: center; border-collapse: collapse;">
  <tr style="border-bottom: 1px solid black;">
    <th>QoS/Partition</th>
    <th>Priority</th>
    <th>MaxWall</th>
    <th>MaxNodesPU</th>
    <th>MaxJobsPU</th>
    <th>MaxSubmitPU</th>
    <th>MaxTRES</th>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>regular</td>
    <td>200</td>
    <td>1-00:00:00</td>
    <td>24</td>
    <td>50</td>
    <td></td>
    <td></td>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>test</td>
    <td>500</td>
    <td>00:10:00</td>
    <td>2</td>
    <td>2</td>
    <td>2</td>
    <td></td>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>long</td>
    <td>200</td>
    <td>2-00:00:00</td>
    <td>24</td>
    <td>20</td>
    <td></td>
    <td></td>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>xlong</td>
    <td>200</td>
    <td>8-00:00:00</td>
    <td>6</td>
    <td>14</td>
    <td></td>
    <td></td>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>large</td>
    <td>200</td>
    <td>2-00:00:00</td>
    <td>40</td>
    <td>6</td>
    <td></td>
    <td></td>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>xlarge</td>
    <td>200</td>
    <td>2-00:00:00</td>
    <td>80</td>
    <td>6</td>
    <td></td>
    <td></td>
  </tr>
  <tr style="border-bottom: 1px solid black;">
    <td>serial</td>
    <td>200</td>
    <td>2-00:00:00</td>
    <td>24</td>
    <td>120</td>
    <td></td>
    <td>cpu=1<br/>gpu=1<br/>node=1</td>
  </tr>
</table>

<br> <!-- Blank line -->
This is what each columns means:

- MaxWall: Maximum amount of time the job is allowed to run. ´1-00:00:00´ reads as one day or 24 hours.
- MaxNodesPU: Maximum amount of nodes user's jobs can use at a given time.
- MaxJobsPU: Maximum number of running jobs per user.
- MaxSubmitPU: Maximum number of jobs that can be submitted to the QoS/partition.
- MaxTRES: The maximum number of Trackable RESources (TRES) each job is able to use. 

