<template>
    <section class="vh-100 gradient-custom">

        <div class=" login-box">

            <div class=" flex flex-column justify-center my-4">
                <a href="/" class="centralizar">
                    <img :src="logo" alt="Sistema de Empréstimo" class="h-10 flex justify-center">
                    <h2 class="m-2 text-center">STE</h2>
                </a>
            </div>
            <!-- <p class="text-white-50 mb-5">
                                Insira seu usuário e senha!
                            </p> -->
            <form class="flex justify-center p-2 text-center" @submit.prevent="handleLogin">
                <div data-mdb-input-init class="form-outline form-white mb-4 ">
                    <div class="user-box">
                        <input id="typeEmailX" v-model="name" type="text" required class="form-control form-control-lg">
                        <label>Usuário</label>
                    </div>
                </div>
                <div data-mdb-input-init class="form-outline form-white mb-4">
                    <div class="user-box">
                        <input id="typePasswordX" v-model="password" type="password" required
                            class="form-control form-control-lg">
                        <label>Senha</label>
                    </div>
                </div>
                <!-- <button data-mdb-button-init data-mdb-ripple-init class="btn btn-outline-light btn-lg px-5"
                            type="submit">
                            Login
                        </button> -->

                <div>
                    <p class="mb-0">
                        <button type="submit" class="btn btn-outline-dark btn-lg px-5 fw-bold">Login</button>
                    </p>
                </div>
            </form>
        </div>
    </section>
</template>

<script>
import { login } from '@/services/auth';
import { toast } from 'vue3-toastify';
import logo from '@/assets/logo.svg';
export default {
    data() {
        return {
            name: '',
            password: '',
            logo
        }
    },
    methods: {
        async handleLogin() {
            try {
                await login(this.name, this.password);
                toast.success('Login com sucesso!', { autoClose: 1000 });
                this.$router.push('/');
            } catch (error) {
                toast.error('Usuário ou senha inválido!', { autoClose: 1000 });
                console.error('Erro ao fazer login', error);
            }
        }
    }
}
</script>

<style scoped>
html {
    height: 100vh;
}

.centralizar {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-decoration: none;
}

.centralizar a {
    text-decoration: none;
    text-decoration-style: none;
}

.centralizar img {
    align-self: center;
}

.login-box {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 400px;
    height: fit-content;
    transform: translate(-50%, -50%);
    background: #fff;
    box-sizing: border-box;
    box-shadow: 0 15px 25px rgba(0, 0, 0, .6);
    border-radius: 10px;
}

.login-box h2 {
    margin: 0 0 30px;
    padding: 0;
    color: #000;
    text-align: center;
}

.login-box .user-box {
    position: relative;
}

.login-box .user-box input {
    width: 100%;
    padding: 10px 0;
    font-size: 16px;
    color: #000;
    margin-bottom: 30px;
    border: none;
    border-bottom: 1px solid #000;
    outline: none;
    background: transparent;
    text-decoration-style: none;
}

.login-box .user-box label {
    position: absolute;
    top: 0;
    left: 0;
    padding: 10px 0;
    font-size: 16px;
    color: #000;
    pointer-events: none;
    transition: .5s;
}

.login-box .user-box input:focus~label,
.login-box .user-box input:valid~label {
    top: -20px;
    left: 0;
    color: #004062;
    font-size: 12px;
}

.login-box form a {
    position: relative;
    display: inline-block;
    padding: 10px 20px;
    color: #004062;
    font-size: 14px;
    text-decoration: none;
    text-transform: uppercase;
    overflow: hidden;
    transition: .5s;
    margin-top: 20px;
    letter-spacing: 4px;
    text-align: center;
}
</style>