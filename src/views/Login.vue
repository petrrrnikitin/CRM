<template>
    <form class="card auth-card" @submit.prevent="submitHandler">
        <div class="card-content">
            <span class="card-title">Домашняя бухгалтерия</span>
            <div class="input-field">
                <input  v-model.trim="email"
                        :class="{invalid: ($v.email.$dirty && !$v.email.required) || ($v.email.$dirty && !$v.email.email)}"
                        id="email"
                        type="text"
                >
                <label for="email">Email</label>
                <small  v-if="$v.email.$dirty && !$v.email.required"
                        class="helper-text invalid">Поле email не должно быть пустым</small>
                <small  v-else-if="$v.email.$dirty && !$v.email.email"
                        class="helper-text invalid">Введите корректный e-mail</small>
            </div>
            <div class="input-field">
                <input  v-model.trim="password"
                        :class="{invalid: ($v.password.$dirty && !$v.password.required) || ($v.password.$dirty && !$v.password.minLength)}"
                        id="password"
                        type="password"
                >
                <label for="password">Пароль</label>
                <small v-if="($v.password.$dirty && !$v.password.required)" class="helper-text invalid">Введите пароль</small>
                <small v-else-if="($v.password.$dirty && !$v.password.minLength)" class="helper-text invalid">Пароль должен быть 8 символов. Сейчас он {{password.length}}</small>
            </div>
        </div>
        <div class="card-action">
            <div>
                <button
                        class="btn waves-effect waves-light auth-submit"
                        type="submit"
                >
                    Войти
                    <i class="material-icons right">send</i>
                </button>
            </div>

            <p class="center">
                Нет аккаунта?
                <router-link to="/register">Зарегистрироваться</router-link>
            </p>
        </div>
    </form>
</template>

<script>
    import {email, required, minLength} from 'vuelidate/lib/validators'

    export default {
        name: "Login",
        data: () => ({
            email: '',
            password: '',
        }),
        validations: {
            email: {email, required},
            password: {required, minLength: minLength(8)}
        },
        methods: {
            submitHandler() {
                if (this.$v.$invalid) {
                    this.$v.$touch()
                    return
                }
                const formData = {
                    email: this.email,
                    password: this.password
                }
                console.log(formData)
                this.$router.push('/')
            }
        }
    }
</script>

<style scoped>

</style>