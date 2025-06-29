<!--  -->
  <details class="main-item">
    <summary>Learned Cardinality</summary>
    <p>
        database cardinality estimation predicts the number of rows returned by a database query (i.e., a SQL statement), which will then influence the query optimization plans. Traditional cardinality estimation relies on heuristics and domain knowledge; whereas, the learned cardinalities learn from the trace data. The inputs of learned cardinalities are SQL queries, and the outputs are estimated number of returned rows.
        For more information, check out the <a href="https://arxiv.org/pdf/1809.00677">paper</a>.
    </p>
    <details class="nested-item">
      <summary>Neural Network</summary>
          <details class="nested-item">
        <summary>Original Paper</summary>
        <p>
The paper proposes MSCN (Multi-Set Convolutional Network) for cardinality estimation. It uses three two-layer neural networks to process different parts of a SQL query: tables, joins, and predicates. Each part goes through a shared MLP:
      <br><br>
      &nbsp;&nbsp;&nbsp;&nbsp;- <code>Linear → ReLU → Linear → ReLU</code><br><br>
      The outputs from each set are averaged, then merged and passed into a final output network:
      <br><br>
      &nbsp;&nbsp;&nbsp;&nbsp;- <code>Linear → ReLU → Linear → Sigmoid</code><br><br>
      This design helps the model handle different query structures and capture complex data patterns. It works better than traditional sampling methods, especially when no qualifying samples exist. The model is small (about 2–3MB) and trained with q-error as the loss.
        </p>
      </details>
    <details class="nested-item">
        <summary>Our Implementation</summary>
        <p>
We use neural networks to learn database query patterns. We implemented four variations of our SetConv architecture:<br>

1. MSCN-128d:<br>
   - Width: 128 neurons per hidden layer<br>
   - Depth: 2 hidden layers in each feature path + 2 layers for combined features<br>
   - Training: 10,000 queries, 10 epochs, batch size of 1024, learning rate of 0.01<br>

2. MSCN-128d-dual:<br>
   - Width: 128 neurons per hidden layer<br>
   - Depth: 2 hidden layers in each feature path + 2 layers for combined features<br>
   - Processing: Dual parallel paths with subtraction operation for final output<br>
   - Training: 10,000 queries, 10 epochs, batch size of 1024, learning rate of 0.01<br>

3. MSCN-2048d:<br>
   - Width: 2048 neurons per hidden layer<br>
   - Depth: 2 hidden layers in each feature path + 2 layers for combined features<br>
   - Training: 10,000 queries, 10 epochs, batch size of 1024, learning rate of 0.01<br>

4. MSCN-2048d-dual:<br>
   - Width: 2048 neurons per hidden layer<br>
   - Depth: 2 hidden layers in each feature path + 2 layers for combined features<br>
   - Processing: Dual parallel paths with subtraction operation for final output<br>
   - Training: 10,000 queries, 10 epochs, batch size of 1024, learning rate of 0.01<br>

Our model processes input features of varying dimensions: sample features (based on table vectors), predicate features (combining column vectors, operation vectors, and values), and join features. Each feature type is processed through its own two-layer MLP with ReLU activations before being combined. We face the same challenges as the original paper and train our models via a training-verification loop to ensure model accuracy and generalization.<br>
        </p>
      </details>
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
