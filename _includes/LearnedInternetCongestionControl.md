<!--  -->
  <details class="main-item">
    <summary>Learned Internet Congestion Control</summary>
    <p>
        congestion control protocols are to ensure efficient data transmission and prevent packet congestion in a network. Learned congestion control studies the patterns of congestion and non-congestion conditions, takes network conditions as input, and decides sending rates in the near future.
        For more information, check out the <a href="https://proceedings.mlr.press/v97/jay19a/jay19a.pdf">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>

      <details class="nested-item">
        <summary>Original Paper</summary>
        <p>
        The neural network (NN) described in the Aurora paper is a small, fully connected neural network with the following architecture: <br>
        - Two hidden layers consisting of 32 and 16 neurons, respectively.<br>
        - The activation function used is the hyperbolic tangent (tanh).

        <br><br>
        Input:
          The input is a tensor with K history, each time step contains the following features:<br>
          1. Latency gradient: latency/time<br>
          2. Latency ratio: Current MI's mean latency / observed mean latency of any MI<br>
          3. Sending ratio: packets sent / packets acknowledged by the receiver<br>
        All the input tensors are flattened into a 1D tensor.
        <br><br>
        Output:<br>
        1. Change of Sending rate: positive value means increase, negative value means decrease<br>
        </p>
      </details>

      <details class="nested-item">
        <summary>Our Implementation</summary>
        <p>
          In our benchmark, considering the limitation of current verifiers, we implement a compatible version of this neural network architecture. Implementation can be found in our <a href="https://github.com/shuyilinn/NN4Sys_Benchmark/blob/main/Models/Aurora/model_benchmark.py">repository</a>.

          <br><br>

          To create different difficulty of the verification, we provide 3 different sizes of the model:
          <br>
          - Small model:
          2 hidden layers of 16 → 8 neurons, tanh nonlinearity.
          <br>

          
          - Mid model (same as original paper):
          2 hidden layers of 32 → 16 neurons, tanh nonlinearity. <br>
          
          - Big model:
          2 hidden layers of 32 → 16 neurons, tanh nonlinearity.
          <br>

          </p>



      </details>

        

    </details>

    <details class="nested-item">
      <summary>Specification</summary>
      <p>
      <strong>AdaptiveBitrate_spec1/2:</strong> When facing good (bad) downloading conditions, the video streaming system should not
        pick the worst (best) video resolution. <br>
      <strong>AdaptiveBitrate_spec3:</strong> Better downloading conditions implies better resolutions
      
      
      
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
        <td>abcrown</td>
        <td>pensieve_big_1</td>
        <td>10</td>
        <td>0</td>
        <td>5.99909349</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_big_2</td>
        <td>10</td>
        <td>0</td>
        <td>6.06507417</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_big_3</td>
        <td>10</td>
        <td>0</td>
        <td>8.87928039</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_mid_1</td>
        <td>10</td>
        <td>0</td>
        <td>6.26007705</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_mid_2</td>
        <td>10</td>
        <td>0</td>
        <td>6.02888779</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_mid_3</td>
        <td>10</td>
        <td>0</td>
        <td>8.6088345</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_small_1</td>
        <td>10</td>
        <td>0</td>
        <td>5.0981046</td>
        <td>0</td>
      </tr>
      <tr>
        <td>marabou</td>
        <td>pensieve_small_1</td>
        <td>10</td>
        <td>0</td>
        <td>1.90850646</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_small_2</td>
        <td>10</td>
        <td>0</td>
        <td>5.00802932</td>
        <td>0</td>
      </tr>
      <tr>
        <td>marabou</td>
        <td>pensieve_small_2</td>
        <td>10</td>
        <td>0</td>
        <td>1.91794796</td>
        <td>0</td>
      </tr>
      <tr>
        <td>abcrown</td>
        <td>pensieve_small_3</td>
        <td>10</td>
        <td>0</td>
        <td>6.80163713</td>
        <td>0</td>
      </tr>
    </tbody>
</table>
</details>

  </details>
