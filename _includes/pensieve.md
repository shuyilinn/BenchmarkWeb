<!--  -->
  <details class="main-item">
    <summary>Learned Adaptive Bitrate</summary>
    <p>
        In video streaming, adaptive bitrate algorithms are used on client-side video players to decide the
        resolution (e.g., 720P) to download for the next video chunk. Learned adaptive bitrate uses neural
        networks to select future video chunks based on observations collected by client video players.
        For more information, check out the <a href="https://people.csail.mit.edu/hongzi/content/publications/Pensieve-Sigcomm17.pdf">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>

      <details class="nested-item">
        <summary>Original Paper</summary>
        <p>
        The neural network (NN) in the Pensieve paper is a deep feedforward neural network used for adaptive bitrate control in video streaming. It takes multiple input features related to video playback, network conditions, and device performance. These inputs are processed through several hidden layers to predict the optimal video bitrate that maximizes quality while minimizing interruptions like buffering.
        
        <h4>Input:</h4>
          The input is a tensor with N history time steps, each time step contains the following features:
        <ul>
          <li>Last chunk bitrate: bitrate/max bitrate, ex: 360P/1080P</li>
          <li>Past chunk download time</li>
          <li>Next chunk sizes</li>
          <li>Current buffer size</li>
          <li>Number of chunks left: eg: 43/48</li>
          <li>Past chunk throughput: </li>
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
