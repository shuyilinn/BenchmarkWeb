<!--  -->
  <details class="main-item">
    <summary>Learned Bloom Filter</summary>
    <p>
         A bloom filter is a probabilistic data structure that has been widely used in many computer systems. Bloom filters test whether an element (for example, a string) is in a pre-defined set. Bloom filters allow false positives: it may return true for an element that is not in the set. The inputs are being-tested elements, and the outputs are booleans, whether the elements are in the set.
        For more information, check out the <a href="https://dl.acm.org/doi/pdf/10.1145/3183713.3196909">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>


      <details class="nested-item">
        <summary>Original Paper</summary>
        <p>
The original paper introduces Learned Bloom Filter, a compact replacement for traditional Bloom filters that leverages a binary classifier to distinguish between keys and non-keys. The initial implementation uses a recurrent neural network (GRU) with 16 hidden units and a 32-dimensional character embedding to process string inputs. While the model achieves high classification accuracy, it cannot guarantee zero false negatives. To address this limitation, the final design incorporates an auxiliary Bloom filter to catch any missed keys, thereby ensuring correctness while reducing overall memory consumption.
        </p>
      </details>

      <details class="nested-item">
        <summary>Our Implementation</summary>
        <p>
        We use neural networks to learn Bloom filters. Our architecture is as follows:

  - Width: 256 neurons per hidden layer  
  - Depth: 4 layers (3 fully connected layers followed by ReLU activations, and 1 final output layer)  
  - Output: A sigmoid activation is applied to produce a probability indicating key membership  

This model takes a 2-dimensional input and predicts whether a given key belongs to the target set.




        </p>

      </details>

    </details>

    <details class="nested-item">
      <summary>Specification</summary>
      <p>
      The false positive and false negative rates are bounded.

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
            <td>bloom_filter</td>
            <td>10</td>
            <td>0</td>
            <td>3.38892075</td>
            <td>0</td>
        </tr>
        <tr>
            <td>marabou</td>
            <td>bloom_filter</td>
            <td>10</td>
            <td>0</td>
            <td>2.23303003</td>
            <td>0</td>
        </tr>
    </tbody>
</table>

</details>

  </details>
