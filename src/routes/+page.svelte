<script lang="ts">
	import { goto } from '$app/navigation';
	import { auth } from '../utils/firebase';
	import { signInWithPopup, GoogleAuthProvider, onAuthStateChanged } from 'firebase/auth';

	import { Input, Button } from '../lib/components/index';

	let disabled = false;

	async function loginWithGoogle() {
		const provider = new GoogleAuthProvider();

		const result = await signInWithPopup(auth, provider);

		goto('/profile')
			.then(() => {
				console.log('success');
			})
			.catch((error) => {
				console.log(error);
			});
	}
</script>

<svelte:head>
	<title>Login page</title>
</svelte:head>

<div class="vh-100 bg-body-secondary">
	<div class="container h-100">
		<div class="row justify-content-center h-100 align-items-center">
			<div class="col-5 bg-white p-5 shadow rounded">
				<form action="?/submit" method="post" autocomplete="off">
					<Input name="login" label="Login" placeholder="Usuario" required />
					<Input name="password" label="Contraseña" placeholder="Contraseña" required />
					<div class="row mt-3">
						<span class="text-center">
							<a href="/forgot">¿Olvido su contraseña?</a>
						</span>
					</div>
					<div class="d-grid mt-4">
						<Button buttonColor="btn-primary" type="submit" {disabled} text="Login" />
					</div>
				</form>
				<div class="row mt-3">
					<p class="text-center">
						¿No estas registrado? <span><a href="/register">Registrarse</a></span>
					</p>
				</div>

				<div class="d-flex justify-content-center align-items-end" style="height: 35px">
					<p class="text-center align-bottom m-0">Login con</p>

					<button type="button" class="btn" on:click={loginWithGoogle}
						><div style="cursor: pointer">
							<img
								src="https://www.pngmart.com/files/16/Google-Logo-PNG-Image.png"
								style="height: 35px"
								alt=""
							/>
						</div></button
					>
				</div>
			</div>
		</div>
	</div>
</div>
