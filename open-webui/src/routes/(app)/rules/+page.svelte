<script lang="ts">
  import { onMount } from 'svelte';
  import { writable } from 'svelte/store';

  // HTML-контент из backend
  const html = writable('<p>Загрузка...</p>');

  onMount(async () => {
    try {
      const res = await fetch('http://localhost:8080/rules'); 

      if (!res.ok) {
        html.set(`<p>Не удалось загрузить файл. Статус: ${res.status}</p>`);
        return;
      }

      const text = await res.text();
      html.set(text);
    } catch (err) {
      html.set(`<p>Ошибка при загрузке файла: ${err}</p>`);
    }
  });
</script>

<svelte:head>
  <title>Правила</title>
</svelte:head>

<div class="rules-page">
  {@html $html}
</div>

<style>
.rules-page {
  padding: 1rem;
  font-family: Arial, sans-serif;
  line-height: 1.5;
}
</style>
