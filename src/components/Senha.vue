<template>
    <div class="question-title">Questão 1</div>
    <div class="question-title">Processamento de senha:</div>
    <div class="question-text">
        Crie funções de conferência para cada elemento necessário à entrada de senha
        (ao menos um caractere minúsculo, ao menos 8 caracteres, senhas iguais, etc...)
        e exiba os pontos conferidos apenas quando o usuário começar a digitar na caixa
        de texto.
    </div>
	<div class="form-group">
		<label for="senha"> <span>Senha: </span> </label>
        <div class="password">
            <input name="senha" class="form-control" :class="{'valid':passwordValidation.valid}" 
            :type="passwordVisible ? 'text' : 'password'" v-model="password" id="senha" placeholder="Insira sua senha..." required/>
            <button class="visibility" tabindex='-1' @click="togglePasswordVisibility()" :arial-label='passwordVisible ? "Hide password" : "Show password"'>
			<i>{{ passwordVisible ? "ocultar_senha" : "mostrar_senha" }}</i>
		</button>
        </div>

        <label for="senha"> <span> Repita a senha: </span> </label>
        <input name="senhaConf"  v-model.lazy="checkPassword" type="password" placeholder="Repita a senha..." required/>
        <transition name="hint" appear>
		<div v-if='passwordValidation.errors.length > 0 && !submitted' class='hints'>
			<h2>As duas senhas devem ser iguais!</h2>
			<p v-for="error in passwordValidation.errors" :key="error">{{error}}</p>
		</div>
	</transition>
        <div @input="notSamePassqords" class="matches" v-if='notSamePasswords'>
		<p>Senha incorreta, tente novamente</p>
	</div>
    <div class="matches" @click="resetPasswords" v-if='passwordsFilled && !notSamePasswords && passwordValidation.valid'>
        <p class="correct-s"> Senha correta, clique em entrar</p>
	<button class="btn-res">
		Entrar
	</button>
    </div>
</div>    
</template>

<script>
    export default {
        name: "Senha",
        data() {
            return {
			rules: [
				{ message: "Pelo menos um caractere minúsculo.", regex:/[a-z]+/ },
				{ message: "Pelo menos um caractere maiúsculo.",  regex:/[A-Z]+/ },
				{ message: "Pelo menos 8 caracteres.", regex:/.{8,}/ },
				{ message: "Pelo menos um caractere numérico.", regex:/[0-9]+/ },
                { message: "Pelo menos um caractere especial.", regex:/[#?!@$%^&*-]/ }
			],
			password:'',
			checkPassword:'',
			passwordVisible:false,
			submitted:false
		};
     },
       methods: {
		resetPasswords () {
			this.password = ''
			this.checkPassword = ''
			this.submitted = true
			setTimeout(() => {
				this.submitted = false
			}, 2000)
		},
		togglePasswordVisibility () {
			this.passwordVisible = !this.passwordVisible
		}	
	},
	computed: {
		notSamePasswords () {
			if (this.passwordsFilled) {
				return (this.password !== this.checkPassword)
			} else {
				return false;
			}
		},
		passwordsFilled () {
			return (this.password !== '' && this.checkPassword !== '')
		},
		passwordValidation () {
			let errors = []
			for (let condition of this.rules) {
				if (!condition.regex.test(this.password)) {
					errors.push(condition.message)
				}
			}
			if (errors.length === 0) {
				return { valid: true, errors }
			} else {
				return { valid: false, errors }
			}
		}
	}
}
</script>

<style scoped>
 .form-group {
     display: grid;
     margin: 0 auto;
     grid-template-columns: auto 1fr;
     grid-template-rows: auto;
     grid-column-gap: 20px;
     grid-row-gap: 5px;
     width: 80%;
     margin-bottom: 5px;
 }

input[type="password"] {
	line-height: 1.4;
	display: block;
	color: rgba(136, 152, 170, 1);
	font-weight: 300;
	width: 70%;
	height: calc(2.75rem + 2px);
	padding: .620rem .75rem;
	border-radius: .35rem;
	background-color: #fff;
	transition: border-color .4s ease;
	border: 1px solid #cad1d7;
	outline: 0;
}
input[type="password"]:focus {
	border: 2px solid rgba(50, 151, 211, .45);
}

/* Checkmark & Strikethrough --------- */

.is_valid { color: rgba(14, 231, 61, 0.8); }

.is_valid:before { width: 100%; }

.checked { animation: draw 0.5s ease forwards; }

@keyframes draw {
  to { stroke-dashoffset: 0; }
}
 @media screen and (max-width: 800px) {
     .form-group {
         width: calc(100% - 20px);
     }
 }

 .form-group > label {
     display: flex;
     justify-content: center;
     align-content: center;
     flex-direction: column;
 }

 .form-group > label > span {
     width: 100%;
 }
.form-group{
     background-color: #D4DEDF;
     border-radius: 10px;
}
 .form-group > label {
     background-color: #B0C4DE;
     display: flex;
     width: 70%;
     height: 11vh;
     margin: 10px;
     position: relative;
     justify-content: center;
     align-content: center;
     flex-direction: column;
     margin-left: 80px;
     border-radius: 15px 0 0 15px;
 }

 .form-group > label > span {
     width: 50%;
     font-weight: bold;
     display: flex;
     justify-content: center;
     margin-left: auto;
     margin-right: auto;
     font-family: 'Times New Roman', Times, serif;
 }

 .form-group > input {
     border: 1px solid grey;
     border-radius: 5px;
 }

 .conferido {
     color: green !important;
 }

 .hints {
    
    display: block;
    position: relative;
    margin-left: 10px;
    margin-bottom: 10px;
	max-width:400px;
	padding: 1em;
	background:whitesmoke;
    border-radius: 10px;
    color: #3A81C8;
	
	font-size: .9em;
	color:darken(#D4DEDF, 70%);
 }
.hints h2{
		margin: .5em 0 .2em 0;
		color: red;
		font-size: 1.3rem; 
	}
.hints p{
	font-size: 1rem;
	color: #3CB371;
}
    .password {
	display:flex;
	align-items:center;
}
[type=password], [type=text] {
	font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
	line-height: 1.4;
	display: block;
	color: rgba(136, 152, 170, 1);
	font-weight: 300;
	width: 70%;
	margin-left: 10px;
	height: calc(2.75rem + 2px);
	padding: .620rem .75rem;
	border-radius: .35rem;
	background-color: #fff;
	transition: border-color .4s ease;
	border: 1px solid #cad1d7;
	outline: 0;
}
[type=password] {
	letter-spacing:.2em;
}
.visibility {
	all: unset;
	widows: 50px;
	background:whitesmoke;
	display:flex;
	position: relative;
	margin-left: 10px;
	color: #3A81C8;
	padding:2px .4em 0;
	vertical-align:center;
}

input, button {
	padding:6px;
}
input + button {
	font-size: 1em;
}

.matches p{
	display: flex;
	position: relative;
	left: 10px;
    color: red;
    font-weight: bold;
}
.matches .correct-s{
	display: flex;
	position: relative;
	left: 10px;
    color: #2ecc71;
    font-weight: bold;
}
.btn-res{
	display: flex;
    position: relative;
	justify-content: center;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 10px;
	width: 80px;
    border-radius: 5px;
    color: orangered;
    font-weight: bold;
    cursor: pointer;
    background-color: #00FF7F;
}
.btn-res:hover{
	background-color: orangered;
	color: #00FF7F;
	border-bottom: 3px solid #00FF7F;
}
	enter{
		opacity: 0;
		transform:translate3d(-20px,0,0);
	}
	fade-leave-to {
		opacity:0;
		transform:translate3d(0, 20px, 0);
	}
	fade-enter-active {
		transition:300ms;
	}
	fade-leave-active {
		transition:400ms;
	}
</style>
