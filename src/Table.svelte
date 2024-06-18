<script>
  export let employees = [];
</script>

<style>
  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
  }

  tr:nth-child(even) {
    background-color: #f9f9f9;
  }

  tr:hover {
    background-color: #f1f1f1;
  }

  .rewards {
    margin-top: 10px;
    width: 100%;
  }

  .rewards th {
    background-color: #e2e2e2;
  }

  @media (max-width: 768px) {
    table, thead, tbody, th, td, tr {
      display: block;
    }

    th {
      display: none;
    }

    tr {
      margin-bottom: 10px;
    }

    td {
      display: flex;
      justify-content: space-between;
      padding-left: 50%;
      position: relative;
    }

    td::before {
      content: attr(data-label);
      position: absolute;
      left: 0;
      width: 50%;
      padding-left: 10px;
      font-weight: bold;
      background-color: #f2f2f2;
    }
  }
</style>

<table>
  <thead>
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Work Start Date</th>
      <th>Created At</th>
      <th>Updated At</th>
      <th>Rewards</th>
    </tr>
  </thead>
  <tbody>
    {#each employees as employee}
      <tr>
        <td data-label="ID">{employee.id}</td>
        <td data-label="Name">{employee.name}</td>
        <td data-label="Work Start Date">{new Date(employee.work_start_date).toLocaleDateString()}</td>
        <td data-label="Created At">{new Date(employee.created_at).toLocaleString()}</td>
        <td data-label="Updated At">{new Date(employee.updated_at).toLocaleString()}</td>
        <td data-label="Rewards">
          {#if employee.rewards.length > 0}
            <table class="rewards">
              <thead>
                <tr>
                  <th>ID</th>
                  <th>Amount</th>
                  <th>Date</th>
                  <th>Is Paid</th>
                </tr>
              </thead>
              <tbody>
                {#each employee.rewards as reward}
                  <tr>
                    <td data-label="ID">{reward.id}</td>
                    <td data-label="Amount">{reward.amount}</td>
                    <td data-label="Date">{new Date(reward.date).toLocaleDateString()}</td>
                    <td data-label="Is Paid">{reward.is_paid ? 'Yes' : 'No'}</td>
                  </tr>
                {/each}
              </tbody>
            </table>
          {:else}
            No Rewards
          {/if}
        </td>
      </tr>
    {/each}
  </tbody>
</table>
