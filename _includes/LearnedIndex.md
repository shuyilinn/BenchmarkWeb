<!--  -->
  <details class="main-item">
    <summary>Learned Index</summary>
    <p>
        A database index is a data structure that improves data retrieval by linking database keys to their storage positions. Learned indexes replace traditional structures like B-Trees with ML models that predict storage locations based on database keys.
        For more information, check out the <a href="https://dl.acm.org/doi/pdf/10.1145/3183713.3196909">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>
            <details class="nested-item">
        <summary>Original Paper</summary>
        <p>
        The original paper introduces Recursive Model Index (RMI), a framework that leverages a set of machine learning models to construct a hierarchical graph. The final implementation opts for linear models instead of neural networks to enhance execution performance. The initial naive design employs a two-layer fully connected neural network with 32 neurons. However, training a neural network to accurately model the database proves to be challenging.
        </p>
      </details>

    <details class="nested-item">
        <summary>Our Implementation</summary>
        <p>
          We use neural networks to learn database index. We have two sizes of neural networks:<br>
          1. LINN (Lightweight Neural Network):<br>
            - Width: 128 neurons per hidden layer.<br>
            - Depth: 4 layers (3 fully connected layers followed by ReLU activations and 1 output layer).<br>
        2. DeepLINN (Deep Lightweight Neural Network):<br>
            - Width: 128 neurons per hidden layer.<br>
            - Depth: 6 layers (5 fully connected layers with ReLU activations).<br><br>
          
           We face the same challenge as the original paper. We train the models via a 
          <a href="https://naizhengtan.github.io/doc/papers/building23wei.pdf">training-verification loop</a>.


          
          </p>
      </details>

      
       </details>

    <details class="nested-item">
      <summary>Specification</summary>
      <p>
      All predicted data locations are error-bounded.
      
      
      
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
            <td>lindex_0</td>
            <td>10</td>
            <td>0</td>
            <td>3.12916079</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>lindex_0</td>
            <td>10</td>
            <td>0</td>
            <td>0.621874303</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>lindex_1</td>
            <td>10</td>
            <td>0</td>
            <td>6.74826283</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>lindex_2</td>
            <td>10</td>
            <td>0</td>
            <td>72.5362575</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>lindex_deep_0</td>
            <td>10</td>
            <td>0</td>
            <td>3.16443444</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>lindex_deep_0</td>
            <td>10</td>
            <td>0</td>
            <td>1.201228401</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>lindex_deep_1</td>
            <td>10</td>
            <td>0</td>
            <td>7.58243066</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>lindex_deep_2</td>
            <td>7</td>
            <td>0</td>
            <td>92.5729578</td>
            <td>3</td>
        </tr>
    </tbody>
</table>

</details>

  </details>
