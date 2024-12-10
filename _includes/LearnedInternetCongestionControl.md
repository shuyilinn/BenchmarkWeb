<!--  -->
  <details class="main-item">
    <summary>Learned Internet Congestion Control</summary>
    <p>
        Congestion control protocols are to ensure efficient data transmission and prevent packet congestion in a network. Learned congestion control studies the patterns of congestion and non-congestion conditions, takes network conditions as input, and decides sending rates in the near future.
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

      <strong>CongestCtrl_spec101/102:</strong> When observing good (bad) networking conditions, the sender does not decrease (increase) packet sending rates. <br>
      <strong>CongestCtrl_spec2:</strong> When observing better networking conditions, the sender increases packet sending rates by either the same or a larger amount. <br>
      <strong>CongestCtrl_spec3:</strong> When the networking condition changes from bad to good, the sender eventually increases packet sending rates. 
      
      
      
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
            <td>aurora_big_101</td>
            <td>0</td>
            <td>10</td>
            <td>2.19588738</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_big_101</td>
            <td>0</td>
            <td>10</td>
            <td>0.102064294</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_big_102</td>
            <td>6</td>
            <td>4</td>
            <td>2.838494590</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_big_102</td>
            <td>6</td>
            <td>4</td>
            <td>0.09996135</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_big_2</td>
            <td>0</td>
            <td>10</td>
            <td>2.32072963</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_big_2</td>
            <td>0</td>
            <td>10</td>
            <td>0.102983946</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_big_3</td>
            <td>0</td>
            <td>10</td>
            <td>2.22639322</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_big_3</td>
            <td>0</td>
            <td>10</td>
            <td>0.23421416</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_big_4</td>
            <td>0</td>
            <td>10</td>
            <td>2.25798789</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_mid_101</td>
            <td>10</td>
            <td>0</td>
            <td>2.96464823</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_mid_101</td>
            <td>10</td>
            <td>0</td>
            <td>0.042553444</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_mid_102</td>
            <td>0</td>
            <td>10</td>
            <td>2.37557136</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_mid_102</td>
            <td>0</td>
            <td>10</td>
            <td>0.053586597</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_mid_2</td>
            <td>0</td>
            <td>10</td>
            <td>2.24732022</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_mid_2</td>
            <td>0</td>
            <td>10</td>
            <td>0.049091978</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_mid_3</td>
            <td>0</td>
            <td>10</td>
            <td>2.24376578</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>aurora_mid_3</td>
            <td>0</td>
            <td>10</td>
            <td>0.113317223</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>aurora_mid_4</td>
            <td>10</td>
            <td>0</td>
            <td>3.97856824</td>
            <td>0</td>
        </tr>
    </tbody>
</table>

</details>

  </details>
