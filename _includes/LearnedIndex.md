<!--  -->
  <details class="main-item">
    <summary>Learned Index</summary>
    <p>
        A database index is a data structure that improves data retrieval by linking database keys to their storage positions. Learned indexes replace traditional structures like B-Trees with ML models that predict storage locations based on database keys.
        For more information, check out the <a href="https://dl.acm.org/doi/pdf/10.1145/3183713.3196909">paper</a>.
    </p>
    
    <details class="nested-item">
      <summary>Neural Network</summary>
      <p>
      To be added.


      </p>
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
