<script>
  import { onMount } from 'svelte';
  import Table from './Table.svelte';

  let employees = [];
  let currentPage = 1;
  const apiUrl = process.env.VITE_API_URL;

  async function fetchEmployees(page) {
    const response = await fetch(`${apiUrl}?page=${page}`);
    const data = await response.json();
    employees = data.data;
    currentPage = data.current_page;
  }

  onMount(() => {
    fetchEmployees(currentPage);
  });
</script>

<Table {employees} />
