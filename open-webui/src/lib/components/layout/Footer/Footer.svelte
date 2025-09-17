<script lang="ts">
	import { onMount } from 'svelte';

	let isDarkTheme = false;
	let isHerTheme = false;

	onMount(() => {
		const updateTheme = () => {
			isDarkTheme = document.documentElement.classList.contains('dark');
			isHerTheme = document.documentElement.classList.contains('her');
		};

		updateTheme();

		const mediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
		mediaQuery.addEventListener('change', updateTheme);

		return () => mediaQuery.removeEventListener('change', updateTheme);
	});
</script>

<div class="footer h-[5vh]">
    <p class="footer-company">
        © 2025 MARS Russia. Все права защищены.
    </p>
    <p class="footer-links-container">
        <a href="/rules" target="_blank" rel="noopener noreferrer" on:click|stopPropagation>
            Правила использования <i class="fas fa-external-link-alt"></i>
        </a>
        <a href="https://learning-mars.lms-russia.ru/collection-topics/223499" target="_blank" rel="noopener noreferrer" on:click|stopPropagation>
            Тренинг по ИИ <i class="fas fa-external-link-alt"></i> 
        </a>
        <a href="mailto:roman.kuritsyn@effem.com;ivan.frolov.1@effem.com;alexander.shliakhturov@effem.com;mikhail.bystrov@effem.com?subject=[MARS GPT] Сообщение об ошибке" target="_blank" rel="noopener noreferrer" on:click|stopPropagation>
            Сообщить об ошибке <i class="fas fa-external-link-alt"></i> 
        </a>
    </p>
</div>

<style>
	.footer {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 60px;
		padding: 10px 0;
		z-index: 10;
		pointer-events: auto;
	}

	.footer-company,
	.footer-links-container a {
		color: var(--color-gray-950, #111827);
	}

	:global(.dark) .footer-company,
	:global(.dark) .footer-links-container a {
		color: var(--color-gray-200, #e5e7eb);
	}

	:global(.her) .footer-company,
	:global(.her) .footer-links-container a {
		color: #f5d7d0;
	}

	.footer-company {
		font-size: 14px;
		font-weight: 400;
		line-height: 10px;
	}

	.footer-links-container {
		display: flex;
		justify-content: center;
		gap: 20px;
		font-size: 14px;
		font-weight: 400;
		line-height: 20px;
	}

	.footer-links-container a {
		text-decoration: underline;
		cursor: pointer;
	}

	.footer-links-container a:hover {
		opacity: 0.8;
	}

	.footer-links-container a i {
		margin-left: 5px;
		color: inherit;
	}
</style>


<!-- !TODO  
 
Сссылки на 3 политики()
(на сайте юристов будет)

На одной странице:
Правила пользования(static)

FAQ ()

Примеры промптов(20 текстовых и 20 картинок)
раскрывающиеся, карточки


-->
