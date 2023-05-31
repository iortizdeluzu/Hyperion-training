---
title: Advanced
nav: true
---
<style>
.text {
  margin-bottom: 10px;
}
</style>

# Advanced

## Scalability experiments

<div align="justify" class="text">
Scaling experiments are crucial for assessing code scalability and parallel performance. They involve systematically varying computational resources to gain insights into code behavior under different workloads. These experiments provide valuable information, identify limitations, and drive improvements.
</div>

<div align="justify" class="text">
Results serve two key purposes. Firstly, they diagnose code performance by analyzing execution times and speedup as resources increase. This helps identify bottlenecks and optimize code for better performance.
</div>

<div align="justify" class="text">
Secondly, scaling results are necessary for resource allocation requests. Funding agencies require evidence of code scalability and performance to assess resource requirements and potential impact.
</div>

<div align="justify" class="text">
Visualizations like speedup and efficiency plots effectively present scaling results. They illustrate execution time improvement and resource utilization effectiveness.
</div>

<div align="justify" class="text">
In conclusion, scaling experiments are vital for understanding code scalability and parallel performance. They inform optimization efforts and support resource allocation requests. Visualizations aid in communicating results effectively. 
</div>


<style>
  .info-box {
    background-color: #f0f8ff;
    padding: 20px;
    border: 1px solid #e6eaf2;
    border-radius: 4px;
    margin-bottom: 20px;
  }

  .info-box h3 {
    font-size: 20px;
    margin-bottom: 10px;
    color: #0085ff;
  }

  .info-box p {
    font-size: 16px;
    line-height: 1.5;
    color: #333;
  }

  .info-box .additional-info {
    margin-top: 20px;
    padding: 10px;
    background-color: #f9f9f9;
    border: 1px solid #e6eaf2;
    border-radius: 4px;
    display: none; /* Collapsed by default */
  }

  .info-box .additional-info-toggle {
    cursor: pointer;
    color: #0085ff;
    font-weight: bold;
    text-decoration: underline;
  }
</style>

<div class="info-box">
  <h3>Determine best performance from a scalability study</h3>
  <p>
    Consider the following scalability plot for a random application.

{% include figure.html img="scalability_study.png" alt="intro image here" width="75%" %}

At what point would you consider to be peak performance in this example.
<ol>
<li> The point where performance gains are no longer linear</li>
<li> The apex of the curve </li>
<li> The maximum core count</li>
<li> None of the above</li>
</ol>
You may find that a scalability graph may vary if you ran the same code on a different machine. Why?
  </p>
  <div class="additional-info-toggle">Show Solution</div>
  <div class="additional-info">
<ol>
<li>     No, the performance is still increasing, at this point we are no longer achieving perfect scalability.</li>
<li>     Yes, the performance peaks at this location, and one cannot get higher speed up with this set up.</li>
<li>     No, peak performance has already been achieved, and increasing the core count will onlt reduce performance.</li>
<li>     No, although you can run extra benchmarks to find the exact number of cores at which the inflection point truly lies, there is no real purpose for doing so.</li>
</ol> 
<p>
    Tying into the answer for #4, if you produce scalability studies on different machines, they will be different because of the different setup, hardware of the machine. You are never going to get two scalability studies which are identical, but they will agree to some point.
</p>
  </div>
</div>

<script>
  var additionalInfoToggle = document.querySelector('.additional-info-toggle');
  var additionalInfo = document.querySelector('.additional-info');

  additionalInfoToggle.addEventListener('click', function() {
    if (additionalInfo.style.display === 'none' || additionalInfo.style.display === '') {
      additionalInfo.style.display = 'block';
      additionalInfoToggle.textContent = 'Hide Solution';
    } else {
      additionalInfo.style.display = 'none';
      additionalInfoToggle.textContent = 'Show Solution';
    }
  });
</script>

