<template>
	<form class="sign-up" @submit.prevent="checkForm">
		<div class="form-group">
			<label for="login">Логин:</label>
			<input
				id="login"
				class="form-control"
				:class="v$.loginVV.$invalid ? 'is-invalid' : 'is-valid'"
				v-model.trim="loginVV"
			/>
			<p v-if="v$.loginVV.required.$invalid" class="invalid-feedback">
				обязательное поле
			</p>
			<p v-if="v$.loginVV.minLength.$invalid" class="invalid-feedback">
				Должно быть более 5 символов
			</p>
		</div>

		<div class="form-group">
			<label for="login">Почта:</label>
			<input
				id="email"
				v-model.trim="email"
				type="email"
				class="form-control"
				:class="v$.email.$invalid ? 'is-invalid' : 'is-valid'"
			/>

			<p v-if="v$.email.required.$invalid" class="invalid-feedback">
				обязательное поле
			</p>
			<p v-if="v$.email.$invalid" class="invalid-feedback">
				Некорректный email
			</p>
		</div>

		<div class="form-group">
			<label for="login">Пароль:</label>
			<input
				id="password"
				v-model.trim="password"
				type="password"
				class="form-control"
			/>
		</div>

		<div class="form-group">
			<label for="country">Страна проживания:</label>
			<select id="country" class="form-control" v-model="country">
				<option
					v-for="(country, index) in countries"
					:key="index"
					:value="country.value"
				>
					{{ country.label }}
				</option>
			</select>
		</div>

		<div class="form-group">
			<label for="themes">Любимые темы:</label>
			<select id="themes" class="form-control" v-model="theme" multiple>
				<option
					v-for="(theme, index) in themes"
					:key="index"
					:value="theme.value"
				>
					{{ theme.label }}
				</option>
			</select>
		</div>

		<div class="form-group form-check">
			<input
				type="checkbox"
				class="form-check-input"
				id="notification"
				v-model="agreeWithSendEmail"
				value="1"
			/>
			<label class="form-check-label" for="notification"
				>Уведомлять о новых курсах</label
			>
		</div>

		<div class="form-group form-check">
			<input
				type="checkbox"
				class="form-check-input"
				id="notification2"
				v-model="agreeWithSendEmail"
				value="2"
			/>
			<label class="form-check-label" for="notification2"
				>Уведомлять о новых курсах2</label
			>
		</div>

		<div class="flex">
			<div class="form-check">
				<input
					class="form-check-input"
					type="radio"
					value="male"
					name="exampleRadios"
					id="male"
					v-model="gendere"
				/>
				<label class="form-check-label" for="male"> Мужчина </label>
			</div>

			<div class="form-check">
				<input
					class="form-check-input"
					type="radio"
					value="female"
					name="exampleRadios"
					id="female"
					v-model="gendere"
				/>
				<label class="form-check-label" for="female"> Женщина </label>
			</div>
		</div>

		<button type="submit" class="btn btn-primary">Сохранить</button>
	</form>
</template>

<script>
import { required, sameAs, minLength, email } from 'vuelidate/lib/validators'

import useVuelidate from '@vuelidate/core'

export default {
	setup() {
		return { v$: useVuelidate() }
	},
	data() {
		return {
			loginVV: '',
			email: '',
			password: '',
			gendere: 'male',
			agreeWithSendEmail: [],
			country: 'Russia',
			countries: [
				{
					label: 'Россия',
					value: 'Russia',
				},
				{
					label: 'Канада',
					value: 'Canada',
				},
				{
					label: 'США',
					value: 'USA',
				},
			],
			theme: [],
			themes: [
				{
					label: 'Матем',
					value: 'Math',
				},
				{
					label: 'Технологии',
					value: 'IT',
				},
				{
					label: 'Языки',
					value: 'Language',
				},
			],
		}
	},
	validations() {
		return {
			loginVV: {
				required,
				minLength: minLength(5),
				$autoDirty: true,
			},
			email: {
				required,
				email,
				$autoDirty: true,
			},
		}
	},
	methods: {
		checkForm() {
			this.v$.$validate()
			if (!this.v$.$error) {
				console.log('Form successfully submitted.')
			} else {
				console.log('Form failed validation')
			}
		},
	},
}
</script>

<style>
.form-control {
	width: 400px;
}
.form-check {
	margin-right: 10px;
}
button {
	margin-top: 15px;
}
</style>
