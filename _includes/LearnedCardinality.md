<!--  -->
  <details class="main-item">
    <summary>Learned Cardinality</summary>
    <p>
        database cardinality estimation predicts the number of rows returned by a database query (i.e., a SQL statement), which will then influence the query optimization plans. Traditional cardinality estimation relies on heuristics and domain knowledge; whereas, the learned cardinalities learn from the trace data. The inputs of learned cardinalities are SQL queries, and the outputs are estimated number of returned rows.
        For more information, check out the <a href="https://arxiv.org/pdf/1809.00677">paper</a>.
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
       The predicted cardinalities are close to the ground-truth cardinalities from the database.
      A larger-ranged query returns larger cardinality.
      
      
      
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
            <td>mscn_128d</td>
            <td>10</td>
            <td>0</td>
            <td>12.3426136</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>mscn_128d_dual</td>
            <td>10</td>
            <td>0</td>
            <td>35.0842626</td>
            <td>0</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>mscn_2048d</td>
            <td>3</td>
            <td>0</td>
            <td>150.021686</td>
            <td>7</td>
        </tr>
        <tr>
            <td>abcrown</td>
            <td>mscn_2048d_dual</td>
            <td>6</td>
            <td>0</td>
            <td>125.487949</td>
            <td>4</td>
        </tr>
    </tbody>
</table>

</details>

  </details>
