<script lang="ts">
	import { onMount } from 'svelte';
	export let visible: boolean;
	export let onClose: () => void;

	let isDarkTheme = false;
	let isHerTheme = false;
	let trainingConfirmed = false;
	let policyConfirmed = false;

	$: isButtonEnabled = trainingConfirmed && policyConfirmed;

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

{#if visible}
	<div 
		class="backdrop" 
		on:click={onClose}
	>
		<div 
			class="modal" 
			on:click|stopPropagation
		>
			<h2 class="title">
				⚠️ Условия использования ⚠️
			</h2>
	
			<p>
				Следующие условия использования регулируют доступ и использование платформы <strong>MARS GPT</strong>. Используя MARS GPT, ты принимаешь и соглашаешься соблюдать данные условия, а также все применимые политики компании Mars, включая: Политику конфиденциальности, Политику классификации информации, Политику обращения с информацией и Политику ответственного использования ИИ.
			</p>
			<br/>
	
			<p>
				Твой доступ к MARS GPT может быть отозван, если ты будешь действовать с нарушением данных условий или иных применимых политик компании Mars.
			</p>
			<br/>
	
			<p>
				Ты несешь ответственность за весь контент, сгенерированный тобой с использованием MARS GPT и содержащихся в нем приложений.
			</p>
			<br/>
	
			<p>
				При формировании Запросов запрещено использование слов, выражений, изображений, любых иных материалов, противоречащих нормам гуманности, морали, нравственности и этики, в т.ч. оскорблений, распространение угроз, использование любых выражений или материалов дискриминационного, оскорбительного, непристойного или порнографического характера, направленных на унижение человеческого достоинства, разжигание ненависти или вражды, причинение ущерба деловой репутации, репутации товарных знаков и брендов Правообладателя, или иным образом нарушающих права Правообладателя или любых третьих лиц, в том числе Группы компаний Mars в России.
			</p>
			<br/>
	
			<p>
				Твои запросы и результаты, сгенерированные с помощью MARS GPT, могут быть проверены как в автоматическом, так и в ручном режиме в целях предотвращения злоупотреблений и фильтрации контента.
			</p>
			<br/>
	
			<label class="confirmation">
				<input type="checkbox" bind:checked={trainingConfirmed} />
				Я подтверждаю, что прошел тренинг
			</label>
			<br/>
	
			<label class="confirmation">
				<input type="checkbox" bind:checked={policyConfirmed} />
				Я подтверждаю, что ознакомился с политикой об ответственном использовании генеративного ИИ
			</label>
	
			<button 
				class="close-btn" 
				on:click={onClose}
				disabled={!isButtonEnabled}
			>
				Принять и продолжить
			</button>
		</div>
	</div>
{/if}

<style>
	.backdrop {
		position: fixed;
		inset: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 999;
		background-color: rgba(0, 0, 0, 0.5);
	}

	:global(.dark) .backdrop {
		background-color: rgba(0, 0, 0, 0.8);
	}

	:global(.her) .backdrop {
		background-color: rgba(152, 55, 36, 0.7);
	}

	.modal {
		border-radius: 1rem;
		padding: 2rem;
		max-width: 800px;
		max-height: 90vh;
		overflow-y: auto;
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
		background-color: var(--color-white, #ffffff);
	}

	:global(.dark) .modal {
		background-color: var(--color-gray-800, #1a1a1a);
	}

	:global(.her) .modal {
		background-color: #2a1a17;
	}

	.title {
		font-size: 1.5rem;
		margin-bottom: 1rem;
		text-align: center;
		color: var(--color-gray-800, #4e4e4e);
	}

	:global(.dark) .title {
		color: #ffffff;
	}

	:global(.her) .title {
		color: #f5d7d0;
	}

	p {
		font-size: 14px;
		line-height: 1.6;
		text-align: justify;
		color: var(--color-gray-800, #4e4e4e);
	}

	:global(.dark) p {
		color: #d1d1d1;
	}

	:global(.her) p {
		color: #f5d7d0;
	}

	.confirmation {
		display: flex;
		align-items: center;
		font-size: 14px;
		font-weight: bold;
		margin-top: 1rem;
		color: var(--color-gray-800, #4e4e4e);
	}

	:global(.dark) .confirmation {
		color: #d1d1d1;
	}

	:global(.her) .confirmation {
		color: #f5d7d0;
	}

	.confirmation input {
		margin-right: 0.5rem;
	}

	.close-btn {
		margin-top: 1.5rem;
		padding: 0.5rem 1.5rem;
		font-size: 1rem;
		background: #3b82f6;
		color: white;
		border: none;
		border-radius: 0.5rem;
		cursor: pointer;
	}

	.close-btn:disabled {
		background: #cccccc;
		cursor: not-allowed;
	}

	:global(.her) .close-btn {
		background: #983724;
	}

	.close-btn:hover:not(:disabled) {
		background: #2563eb;
	}

	:global(.her) .close-btn:hover:not(:disabled) {
		background: #7a2d1d;
	}

	.modal::-webkit-scrollbar {
		width: 0px;
		height: 0px;
	}

	.modal::-webkit-scrollbar-thumb {
		border-radius: 10px;
	}

	.modal::-webkit-scrollbar-track {
		background: #f1f1f1;
		border-radius: 10px;
	}

	:global(.dark) .modal::-webkit-scrollbar-track {
		background: #333;
	}

	:global(.her) .modal::-webkit-scrollbar-track {
		background: #4a2a24;
	}
</style>