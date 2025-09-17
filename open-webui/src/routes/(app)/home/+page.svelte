<script lang="ts">
	import Chat from '$lib/components/chat/Chat.svelte';
	// import Help from '$lib/components/layout/Help.svelte';
	import DisclaimerModal from '$lib/components/layout/DisclaimerModal/DisclaimerModal.svelte';
	import { user } from '$lib/stores/index';
	import { updateUserInfo, getUserInfo } from '$lib/apis/users';
	import { onMount } from 'svelte';

	let showDisclaimer = false;

	onMount(async () => {
		const token = localStorage.getItem('token');
		if (!token) return;

		// Сначала проверяем localStoarage
		const localAccepted = localStorage.getItem('disclaimer_accepted');
		if (localAccepted === 'true') {
			showDisclaimer = false;
			return;
		}

		// 2. иначе смотрим info у user
		try {
			const info = await getUserInfo(token);
			const accepted = info?.disclaimer_accepted;

			if (accepted === true) {
				showDisclaimer = false;
				localStorage.setItem('disclaimer_accepted', 'true');
			} else {
				showDisclaimer = true;
			}
		} catch (err) {
			console.error('Ошибка получения user info:', err);
			showDisclaimer = true;
		}
	});

	async function acceptDisclaimer() {
		const token = localStorage.getItem('token');
		if (!token) {
			console.error('Нет токена в localStorage');
			return;
		}

		try {
			await updateUserInfo(token, { disclaimer_accepted: true });

			// обновляем localStorage
			localStorage.setItem('disclaimer_accepted', 'true');

			showDisclaimer = false;
		} catch (err) {
			console.error('Ошибка при принятии дисклеймера:', err);
		}
	}
</script>

<!-- <Help /> -->
<Chat />
<DisclaimerModal visible={showDisclaimer} onClose={acceptDisclaimer}/>