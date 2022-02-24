<template>
	<form
		class="all-form"
		@submit.prevent="checkFormAuth"
		v-if="!isValidFormAndRedirect"
	>
		<div class="input-group mb-3">
			<span class="input-group-text">login</span>
			<input
				type="text"
				class="form-control"
				v-model.trim="form.login"
				:class="v$.form.login.$invalid ? 'is-invalid' : 'is-valid'"
			/>
		</div>
		<p v-if="v$.form.login.required.$invalid">
			{{ v$.form.login.required.$message }}
		</p>
		<p v-if="v$.form.login.minLength.$invalid">
			{{ v$.form.login.minLength.$message }}
		</p>
		<p v-if="v$.form.login.maxLength.$invalid">
			{{ v$.form.login.maxLength.$message }}
		</p>

		<div class="input-group mb-3">
			<span class="input-group-text">email</span>
			<input
				type="text"
				class="form-control"
				v-model.trim="form.email"
				:class="v$.form.email.$invalid ? 'is-invalid' : 'is-valid'"
			/>
		</div>
		<p v-if="v$.form.email.required.$invalid">
			{{ v$.form.email.required.$message }}
		</p>
		<p v-if="v$.form.email.$invalid">{{ v$.form.email.email.$message }}</p>

		<div class="input-group mb-3">
			<span class="input-group-text">password</span>
			<input
				type="text"
				class="form-control"
				v-model.trim="form.password"
				:class="v$.form.password.$invalid ? 'is-invalid' : 'is-valid'"
			/>
		</div>
		<p v-if="v$.form.password.required.$invalid">
			{{ v$.form.password.required.$message }}
		</p>
		<p v-if="v$.form.password.minLength.$invalid">
			{{ v$.form.password.minLength.$message }}
		</p>
		<p v-if="v$.form.password.maxLength.$invalid">
			{{ v$.form.password.maxLength.$message }}
		</p>

		<select
			v-model="countryAuth"
			class="form-select"
			aria-label="select country"
		>
			<option
				v-for="(county, index) in countriesAuth"
				:key="index"
				:value="county.value"
			>
				{{ county.label }}
			</option>
		</select>

		<select
			class="form-select"
			v-model="favoriteAuth"
			multiple
			aria-label="multiple select favorite"
			:class="v$.favoriteAuth.$invalid ? 'is-invalid' : 'is-valid'"
		>
			<option
				v-for="(theme, index) in favoritesThemesAuth"
				:key="index"
				:value="theme.value"
			>
				{{ theme.label }}
			</option>
		</select>
		<p v-if="v$.favoriteAuth.maxLength.$invalid">
			{{ v$.favoriteAuth.maxLength.$message }}
		</p>

		<div class="form-check">
			<label class="form-check-label" for="checkboxId"
				>Согласен с правилами</label
			>
			<input
				class="form-check-input"
				type="checkbox"
				v-model="agreeWithRules"
				id="checkboxId"
				:class="!v$.agreeWithRules.$model ? 'is-invalid' : 'is-valid'"
			/>
		</div>
		<p v-if="!v$.agreeWithRules.$model">Прочтите соглашение</p>

		<div class="form-check">
			<input
				tclass="form-check-input"
				type="checkbox"
				id="podpiskiID"
				v-model="podpiskiAgree"
			/>
			<label class="form-check-label" for="podpiskiID"
				>Уведомлять о новых подписках</label
			>
			<p v-if="!v$.podpiskiAgree.$model">
				Выберите, если нужны инфо о подписках
			</p>
		</div>

		<div class="form-check">
			<input
				class="form-check-input"
				type="radio"
				value="man"
				name="genderExamp"
				id="man"
				v-model="genderCheck"
			/>
			<label class="form-check-label" for="man">man</label>
		</div>
		<div class="form-check">
			<input
				class="form-check-input"
				type="radio"
				name="genderExamp"
				id="woman"
				value="woman"
				v-model="genderCheck"
			/>
			<label class="form-check-label" for="woman">woman</label>
		</div>
		<button type="submit">Зарегистрироваться</button>
	</form>
	<h1 v-else="isValidFormAndRedirect">Вы Успешно авторизованы!</h1>
</template>
<script>
import useVuelidate from '@vuelidate/core'
import {
	required,
	email,
	minLength,
	maxLength,
	between,
	minValue,
	maxValue,
} from '@vuelidate/validators'

export default {
	setup() {
		return { v$: useVuelidate() }
	},
	data() {
		return {
			form: {
				login: '',
				email: '',
				password: '',
			},
			isValidFormAndRedirect: false,
			genderCheck: 'man',
			agreeWithRules: true,
			podpiskiAgree: false,
			countryAuth: '',
			countriesAuth: [
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
			favoriteAuth: [],
			favoritesThemesAuth: [
				{ label: 'Math', value: 'Math' },
				{ label: 'Lang', value: 'Lang' },
				{ label: 'Flover', value: 'Flover' },
				{ label: 'Game', value: 'Game' },
				{ label: 'Go', value: 'Go' },
			],
		}
	},
	validations() {
		return {
			form: {
				login: {
					required,
					minLength: minLength(5),
					maxLength: maxLength(8),
					$autoDirty: true,
				},
				email: {
					required,
					email,
					$autoDirty: true,
				},
				password: {
					required,
					minLength: minLength(10),
					maxLength: maxLength(15),
					$autoDirty: true,
				},
			},

			favoriteAuth: {
				maxLength: maxLength(3),
			},
			agreeWithRules: {
				required,
			},
			podpiskiAgree: {
				required,
			},
			genderCheck: {
				required,
			},
		}
	},
	methods: {
		checkFormAuth() {
			this.v$.$validate()
			if (!this.v$.$error) {
				alert('Form successfully submitted.')
				this.isValidFormAndRedirect = true
			} else {
				alert('Form failed validation')
			}
		},
	},
}
</script>
<style>
.all-form {
	width: 400px;
	margin: 15px;
}
</style>
