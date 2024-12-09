

<!--  -->
  <details class="main-item">
    <summary>Learned Distributed System Scheduler</summary>
    <p>
        The System Scheduler is designed for distributed computing systems like Spark. It manages a cluster of machines running multiple jobs, each with tasks that have dependencies. Using neural networks, a learned scheduler optimizes task scheduling to achieve high-level objectives, such as minimizing job completion time. It takes inputs like the status of jobs, tasks, and the cluster, and outputs the next tasks to run. For more information, check out the <a href="https://web.mit.edu/decima/">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>
      

      <details class="nested-item">
        <summary>Original Paper</summary>
        <p>The original neural network architecture consists of three main components:<br><br>

          1. <b>GCN (Graph Convolutional Network)</b><br>
             - Models dependencies between tasks and jobs<br>
             - Captures graph structure of task interdependencies<br><br>
          
          2. <b>GSN (Graph Scheduling Network)</b><br>
             - Builds on the GCN output<br>
             - Focuses on scheduling optimization<br>
             - Predicts optimal task schedules using graph-structured data<br><br>
          
          3. <b>FC (Fully Connected) Layers</b><br>
             - Refines representations from GCN and GSN<br>
             - Outputs final scheduling decisions<br>
             - Determines next tasks to execute<br><br>

          These components work together to enable efficient task scheduling in distributed systems through dynamic, data-driven decisions.</p>
      </details>

      <details class="nested-item">
        <summary>Our Implementation</summary>
        <p>In our benchmark, considering the limitation of current verifiers, we implement a compatible version of this neural network architecture. We implement 2 versions, benchmark version and a version for marabou the verifier. Implementation can be found in our <a href="https://github.com/Khoury-srg/NN4SysBench/blob/main/Models/Decima/model_benchmark.py">repository</a>.

        <details class="nested-item">
          <summary>Benchmark Version</summary>
          <p>
          We integrate the 3 components into a single neural network. The input is the status of jobs, tasks, and the cluster, and the output is the next tasks to execute. 
          <h4>Input:</h4>
          The input to the model is a tensor that is split into several segments:
          
          <ul>
            <li><strong>node_inputs:</strong> Features of the nodes <br>
                <em>Shape: [batch_size, Max_Node, 5]</em></li>
            
            <li><strong>node_valid_mask:</strong> A mask indicating the validity of nodes <br>
                <em>Shape: [batch_size, 1, Max_Node]</em></li>
            
            <li><strong>gcn_mats:</strong> Graph convolution matrices for message passing <br>
                <em>Shape: [batch_size, 8, Max_Node, Max_Node]</em></li>
            
            <li><strong>gcn_masks:</strong> Masks for each graph convolution operation <br>
                <em>Shape: [batch_size, 8, Max_Node, 1]</em></li>
            
            <li><strong>summ_mats:</strong> Summarization matrices for aggregating graph information <br>
                <em>Shape: [batch_size, Max_Node, Max_Node]</em></li>
            
            <li><strong>running_dags_mat:</strong> Running DAG state matrix <br>
                <em>Shape: [batch_size, 1, Max_Node]</em></li>
            
            <li><strong>dag_summ_backward_map:</strong> A backward map for DAG summarization <br>
                <em>Shape: [batch_size, Max_Node, Max_Node]</em></li>
          </ul>
          All the input tensors are flattened into a 1D tensor.

          <h4>Output:</h4>

          <ul>
            <li><strong>Node Outputs:</strong> Prediction scores for each node. Invalid nodes are masked with value 10000.0 <br>
                <em>Shape: [1, node_num]</em></li>

            <li><strong>Job Outputs (Ignored):</strong> Represents executor scores for each job (not used) <br>
                <em>Shape: [1, job_num, total_executor_num]</em></li>
          </ul>







          </p>
        </details>

        <details class="nested-item">
          <summary>Marabou Version</summary>
          <p>
            Most of the architecture is the same as the benchmark version, with a few key differences such as the use of a different graph convolution layer (GraphLayer_marabou) and learnable parameters for matrices like gcn_mats and gcn_masks.
          </p>
        </details>

        
        
        
        
        </p>
      </details>
    </details>

    <details class="nested-item">
      <summary>Specification</summary>
      <p>
      <strong>LearnedSched_spec1:</strong> If job A's input depends on job B's output and job B is not finished, then job A should not be scheduled. <br>
      <strong>LearnedSched_spec2:</strong> A user cannot get their jobs scheduled earlier by requesting more resources for them.
      
      
      
      </p>
    </details>

    <details class="nested-item">
  <summary>Performance of the Verifier</summary>
  <table border="1">
    <thead>
      <tr>
        <th>Verifier</th>
        <th>Type</th>
        <th>Safe</th>
        <th>Unsafe</th>
        <th>Time</th>
        <th>Timeout</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>decima_mid_1</td>
        <td>abcrown</td>
        <td>10</td>
        <td>0</td>
        <td>9.7232395</td>
        <td>0</td>
      </tr>
      <tr>
        <td>decima_mid_1</td>
        <td>marabou</td>
        <td>10</td>
        <td>0</td>
        <td>10.77956162</td>
        <td>0</td>
      </tr>
      <tr>
        <td>decima_mid_2</td>
        <td>abcrown</td>
        <td>8</td>
        <td>1</td>
        <td>26.29458285</td>
        <td>1</td>
      </tr>
      <tr>
        <td>decima_mid_2</td>
        <td>marabou</td>
        <td>0</td>
        <td>0</td>
        <td>180.0</td>
        <td>10</td>
      </tr>
    </tbody>
  </table>
</details>

  </details>