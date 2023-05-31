---
title: Examples
nav: true
---

# Examples

Here we collect different usefull sbatch script examples.


<style>
  .info-box {
    background-color: #f0f8ff;
    padding: 20px;
    border: 1px solid #e6eaf2;
    border-radius: 4px;
    margin-bottom: 20px;
    font-family: Courier, monospace;
  }

  .info-box h3 {
    font-size: 20px;
    margin-bottom: 10px;
    color: #0085ff;
    cursor: pointer;
    font-family: Helvetica, sans-serif; /* Set your desired regular font here */
  }

  .info-box p {
    font-size: 16px;
    line-height: 1.5;
    color: #333;
    font-family: Courier, monospace;
  }

  .info-box .content {
    display: none; /* Collapsed by default */
  }
</style>

<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">Serial</h3>
  <div class="content">
<p><span style="font-family: Helvetica, Arial, sans-serif;"> Serial jobs are tasks that run sequentially on a single processor without parallelization. They are used for workloads that can't be easily parallelized or don't benefit from parallel processing. </span></p>      
<pre>
#!/bin/bash
#SBATCH --job-name=serial_job
#SBATCH --output=output.log
#SBATCH --error=error.log
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1

echo "Running serial job..."
# Your serial job commands go here
    </pre>
  </div>
</div>


<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">MPI</h3>
  <div class="content">
<p><span style="font-family: Helvetica, Arial, sans-serif;"> MPI (Message Passing Interface) is a parallel programming model for distributed memory systems. It enables programs to run across multiple processors, communicating via message passing. </span></p>
<pre>
#!/bin/bash
#SBATCH --partition=regular
#SBATCH --job-name=JOB_NAME
#SBATCH --cpus-per-task=1
#SBATCH --mem=200gb
#SBATCH --nodes=8
#SBATCH --ntasks-per-node=48

module load program/program_version

mpirun -np $SLURM_NTASKS binaryi < input 
</pre>
  </div>
</div>



<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">OpenMP</h3>
  <div class="content">
<p><span style="font-family: Helvetica, Arial, sans-serif;"> For a OpenMP application the number of threads can be controlled defining the <code>OMP_NUM_THREADS</code> or SLURM's <code>--cpus-per-task</code> job directive. If this variable is not defined, the number of threads created will be equal to the amount of cores reserved in your cpuset, that is, the number of cores requested in the batch script. </span></p>
<pre>
#!/bin/bash
#SBATCH --partition=regular
#SBATCH --job-name=JOB_NAME
#SBATCH --cpus-per-task=48
#SBATCH --mem=200gb
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1

module load program/program_version

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

binary < input
</pre>
  </div>
</div>

<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">Hybrid (MPI+OpenMP)</h3>
  <div class="content">
<p><span style="font-family: Helvetica, Arial, sans-serif;"> Hybrid parallelization, combining MPI (Message Passing Interface) and OpenMP, is a powerful approach for harnessing the computational capabilities of both distributed and shared memory systems. In this paradigm, MPI is used for inter-node communication, enabling data exchange and synchronization between distributed processes, while OpenMP is employed within each node for intra-node parallelization across multiple threads. </span></p>
<pre>
#!/bin/bash
#SBATCH --partition=regular
#SBATCH --job-name=JOB_NAME
#SBATCH --cpus-per-task=4
#SBATCH --mem=200gb
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=12

module load program/program_version

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
mpirun -np $SLURM_NTASKS binaryi < input
</pre>
  </div>
</div>


<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">GPU jobs</h3>
  <div class="content">
<p><span style="font-family: Helvetica, Arial, sans-serif;">GPU jobs refer to tasks or applications that utilize the computational power of Graphics Processing Units (GPUs) for accelerated processing. GPU jobs are commonly used for deep learning, scientific simulations, data analytics, and other computationally intensive tasks that can benefit from parallel processing on GPUs. By leveraging the power of GPUs, these jobs can achieve significant performance gains compared to running on CPUs alone.One can request the usage of GPUs by adding <code>#SBATCH --gres=gpu:p40:X</code> to the submision script. In the following example we request 2 GPUs per node </span></p>
<pre>
#!/bin/bash
#SBATCH --partition=regular
#SBATCH --job-name=GROMACS_job
#SBATCH --mem=200gb
#SBATCH --cpus-per-task=1
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=8
#SBATCH --gres=gpu:p40:2
#SBATCH --output=%x-%j.out
#SBATCH --error=%x-%j.err

module load GROMACS/2020-fosscuda-2019b

srun gmx_mpi mdrun -ntomp $SLURM_CPUS_PER_TASK -nb auto -bonded auto -pme auto -gpu_id 01 -s input.tpr
</pre>
  </div>
</div>

<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">Job Array</h3>
  <div class="content">
<p><span style="font-family: Helvetica, Arial, sans-serif;">SLURM job arrays allow users to submit and manage a group of related jobs as a single entity. A job array consists of multiple tasks that are similar in nature but have different input data or parameters. SLURM handles the task distribution, resource allocation, and job dependencies automatically. They simplify job submission and management, improve efficiency, and provide better control over large-scale job execution in HPC environments. </span></p> 
      <pre>
#!/bin/bash
#SBATCH --partition=regular
#SBATCH --job-name=ARRAY_JOB
#SBATCH --time=00:10:00
#SBATCH --nodes=1              # nodes per instance
#SBATCH --ntasks=1             # tasks per instance
#SBATCH --array=0-9           # instance indexes
#SBATCH --output=%x-%j.out
#SBATCH --error=%x-%j.err

echo "Slurm job id is ${SLURM_JOB_ID}"
echo "Array job id is ${SLURM_ARRAY_JOB_ID}"
echo "Instance index is ${SLURM_ARRAY_TASK_ID}."    
</pre>
  </div>
</div>


<div class="info-box">
  <h3 onclick="toggleInfoBox(this)">Dependency chains</h3>
  <div class="content">
   <p><span style="font-family: Helvetica, Arial, sans-serif;">Job dependencies are used to defer the start of a job until some dependencies have been satisfied. Job dependencies can be defined using the <code>--dependency</code> argument of the <code>sbatch</code> command:
<br>
    <code>#SBATCH --dependency="dependency_type"</code>
   <br>
   <br>
    Available dependencies are:
   <br>
    - <code>after:jobID</code> job starts when job with <code>jobID</code> begun execution.
   <br>
    - <code>afterany:jobID</code> job starts when job with <code>jobID</code> terminates.
   <br>
    - <code>aferok:jobID</code> job starts when job with <code>jobID</code> terminates successfully.
   <br>
    - <code>afternook:jobID</code> job starts when job with <code>jobID</code> terminates with non-zero status.
   <br>
    - <code>singleton:jobID</code> jobs starts when any previously job with the same job name and user terminates. This can be used to chain restartable jobs.
   
      <pre>
#!/bin/bash
#SBATCH --partition=regular
#SBATCH --job-name=ARRAY_JOB
#SBATCH --time=00:10:00
#SBATCH --nodes=1              # nodes per instance
#SBATCH --ntasks=1             # tasks per instance
#SBATCH --array=0-9           # instance indexes
#SBATCH --output=%x-%j.out
#SBATCH --error=%x-%j.err

echo "Slurm job id is ${SLURM_JOB_ID}"
echo "Array job id is ${SLURM_ARRAY_JOB_ID}"
echo "Instance index is ${SLURM_ARRAY_TASK_ID}."
</pre>



<script>
  function toggleInfoBox(element) {
    var content = element.nextElementSibling;
    if (content.style.display === 'none' || content.style.display === '') {
      content.style.display = 'block';
    } else {
      content.style.display = 'none';
    }
  }
</script>
