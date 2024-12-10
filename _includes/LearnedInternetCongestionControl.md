<!--  -->
  <details class="main-item">
    <summary>Learned Adaptive Bitrate</summary>
    <p>
        congestion control protocols are to ensure efficient data transmission and prevent packet congestion in a network. Learned congestion control studies the patterns of congestion and non-congestion conditions, takes network conditions as input, and decides sending rates in the near future.
        For more information, check out the <a href="https://proceedings.mlr.press/v97/jay19a/jay19a.pdf">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>

      <details class="nested-item">
        <summary>Original Paper</summary>
        <p>
        The neural network (NN) in the Aurora paper is a small fully connected neural network. The architecture is 2 hidden layers conposed of 32->16 neurons and tanh nonlinearigy.
        
        <h4>Input:</h4>
          The input is a tensor with N history time steps, each time step contains the following features:
        <ul>
          <li>Latency gradient: latency/time</li>
          <li>Latency ratio: Current MI’s mean latency / observed mean latency of any MI</li>
          <li>Sending ratio: packets sent / packets acknowledged by the receiver</li>
        </ul>
        All the input tensors are flattened into a 1D tensor.
        <h4>Output:</h4>
        <ul>
          <li>optimal video bitrate</li>
        </ul>
        </p>
      </details>

      <details class="nested-item">
        <summary>Our Implementation</summary>
        <p>
          In our benchmark, considering the limitation of current verifiers, we implement a compatible version of this neural network architecture. We implement 2 versions, benchmark version and a version for marabou the verifier. Implementation can be found in our <a href="https://github.com/Khoury-srg/NN4SysBench/blob/main/Models/Pensieve/model_no_softmax_no_argmax.py">repository</a>.
        </p>

        <details class="nested-item">
          <summary>Benchmark Version</summary>
          <p>
            The model is almost the same as the original paper, except that we remove the softmax and argmax layers, and all the input tensors are flattened into a 1D tensor. The input and output can be referred to in the Original Paper section.   <br>

            To create different difficulty of the verification, we provide 3 different sizes of the model:
          

          <div class="model-variant">
            <h4>Small model:</h4>
            <ul>
              <li>First Layer: 4 parallel fully connected layers, each containing 128 neurons</li>
              <li>Second Layer: A fully connected (linear) layer with 128 neurons</li>
              <li>Output Layer: Fully connected (linear) layer with 6 neurons</li>
            </ul>
          </div>

          <div class="model-variant">
            <h4>Mid model (same as original paper):</h4>
            <ul>
              <li>First Layer: 3 parallel fully connected layers, each containing 128 neurons, and a 1D convolution layer with 128 filters and kernel size 4. These 4 layers take the input features in parallel.</li>
              <li>Second Layer: A fully connected (linear) layer with 128 neurons</li>
              <li>Output Layer: A fully connected (linear) layer with 6 neurons</li>
            </ul>
          </div>

          <div class="model-variant">
            <h4>Big model:</h4>
            <ul>
              <li>First Layer: 3 parallel fully connected layers, each containing 128 neurons, and a 1D convolution layer with 128 filters and kernel size 4. These 4 layers are parallel.</li>
              <li>Second Layer: A fully connected (linear) layer with 256 neurons</li>
              <li>Output Layer: Fully connected (linear) layer with 6 neurons</li>
            </ul>
          </div>
          </p>
        </details>

        <details class="nested-item">
          <summary>Marabou Version</summary>
          <p>
            Main difference:

          <ul>
            <li>Use torch.split() to split the input tensor into 2 parts.</li>
          </ul>
          </p>
        </details>
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
