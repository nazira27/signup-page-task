<template>
    <div class="wrapper">
        <div class="card">
            <h4>Регистрация</h4>
            <span >Уже есть аккаунт? <a href="#">Войти</a></span>
            <div style="margin-top: 32px">
                <label>Имя</label><br>
                <input required class="inputs" type="text" id="name" name="name" placeholder="Введите Ваше имя"  @blur="validateEmail">
            </div>
            <div>
                <label>Email</label><br>
                <input required v-model="email" class="inputs" type="text" id="email" name="email" placeholder="Введите ваш email">
                <br><span class="error-validate">{{ msg }}</span>
            </div>
            <div>
                <label>Номер телефона</label><br>
                <input required v-model="phone" class="inputs" type="text" id="phone" name="phone" @input="acceptNumber" placeholder="Введите номер телефона">
            </div>
             <div class="dropdown custom-select">
                <label>Язык</label><br>
                <button @click="dropdownOpen" class="dropbtn" :style="selectedLang==='' ? 'color: #7C9CBF' : ''"> {{selectedLang!=='' ? selectedLang : 'Язык'}}</button>
                <div class="dropdown-content" id="dropdown">
                    <a href="#" @click="changeLang(1)">Русский</a>
                    <a href="#" @click="changeLang(2)">Английский</a>
                    <a href="#" @click="changeLang(3)">Китайский</a>
                    <a href="#" @click="changeLang(4)">Испанский</a>
                </div>
            </div>
            <div style="display: flex">
                <input v-model="checkbox" type="checkbox" id="vehicle1" name="vehicle1" value="Bike" class="check-box">
                <p style="font-size: 14px; color: #756F86; margin: 3px 0">Принимаю <a>условия</a> использования</p><br>
            </div>
            <button :class="!checkbox ? 'btn' : 'btn-active'" :disabled="!checkbox">Зарегистрироваться</button>
        </div>
    </div>
</template>
<script>

export default {
    name:"SignUp",
    data() {
        return {
            selectedLang: '',
            checkbox: false,
            disabled: true,
            msg: '',
            email: '',
            phone: '',
            reg: /^(([^<>()\]\\.,;:\s@"]+(\.[^<>()\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/
        }
    },
    watch: {
        email(value) {
            if (!this.reg.test(value) || !this.reg.test(this.email)) {
                this.msg = 'Введено не корректное значение';
            } else {
                this.msg = '';
            }
        }
    },
    methods: {
        acceptNumber() {
            var x = this.phone.replace(/\D/g, '').match(/(\d{0,4})(\d{0,3})(\d{0,4})/);
            this.phone = !x[2] ? x[1] : '(+' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
        },
        validateEmail() {
            if (this.reg.test(this.email)) {
                this.msg = 'Введено не корректное значение';
            } else {
                this.msg = '';
            }
        },
        dropdownOpen() {
            document.getElementById("dropdown").style.display = "block";
        },
        changeLang(id) {
            if (id === 1) {
                this.selectedLang = 'Русский'
            } else if (id === 2) {
                this.selectedLang = 'Английский'
            } else if (id === 3) {
                this.selectedLang = 'Китайский'
            } else if (id === 4) {
                this.selectedLang = 'Испанский'
            }
            document.getElementById("dropdown").style.display = "none";
        }
    }
}
</script>
<style scoped>
.check-box {
    margin-right: 5px !important;
    width: 24px;
    height: 24px;
    padding: 0;
    margin: 0;
}
label {
    font-family: IBM Plex Sans;
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 21px;
    color: #756F86;
}
.error-validate {
    font-size: 14px;
    line-height: 18px;
    color: #FF7171;
}
.wrapper {
    min-height: 100vh;
}
.btn-active {
    width: 100%;
    color: #EBF4F8;
    padding: 5px 10px;
    background: #0880AE;
    box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08), 0px 4px 8px rgba(44, 39, 56, 0.08);
    border-radius: 6px;
    height: 56px;
    border: none;
    cursor: pointer;
    font-size: 16px;
}
.btn-active:focus {
    outline: none;
}
.btn {
    border: none;
    font-size: 16px;
    height: 56px;
    width: 100%;
    color: #B1B5BF;
    padding: 5px 10px;
    background: #DBE2EA;
    box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08), 0px 4px 8px rgba(44, 39, 56, 0.08);
    border-radius: 6px;
}
.dropbtn::after {
    margin-top: 5px;
    content: "";
    border: 0.35rem solid transparent;
    border-top-color:#0880AE;
    transform: translateY(0.15em);
    position: absolute;
    right: 10px;
}

.dropbtn {
    height: 52px;
    display: inline-flex;
    text-align: inherit;
    padding: 16px;
    width: 100%;
    background: #FFFFFF;
    border: 1px solid #DBE2EA;
    box-sizing: border-box;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    border-radius: 6px;
}

.dropdown {
    width: 100%;
    position: relative;
    display: inline-block;
}

.dropdown-content {
    margin-top: 2px;
    width: 100%;
    background: #FFFFFF;
    border: 1px solid #DBE2EA;
    box-sizing: border-box;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04), 0px 20px 20px rgba(44, 39, 56, 0.04);
    border-radius: 6px;
    display: none;
    position: absolute;
    min-width: 160px;
    z-index: 1;
    margin-bottom: 10px;
}

.dropdown-content a {
    height: 20px;
    font-size: 16px;
    border-radius: 6px; 
    color: black;
    padding: 12px 9px;
    text-decoration: none;
    display: block;
}

.dropdown-content a:nth-child(1):hover {
    background: #EBF4F8;
    border-radius: 6px 6px 0 0 ;
}
.dropdown-content a:nth-child(3):hover {
    background: #EBF4F8;
    border-radius: 0;
}
.dropdown-content a:nth-child(2):hover {
    background: #EBF4F8;
    border-radius: 0;
} 
.dropdown-content a:nth-child(4):hover {
    background: #EBF4F8;
    border-radius: 0 0 6px 6px;
}

.select-items div:hover, .same-as-selected {
    font-size: 16px;
    border-radius: 6px; 
  background-color: #EBF4F8;
}

.card div {
    margin-bottom: 18px;
}
::placeholder {
    font-size: 16px;
    color: #7C9CBF;
    line-height: 21px;
    opacity: 1; /* Firefox */
}
input:focus, .dropbtn:focus {
    background: #FFFFFF;
    outline: none;
    border: 2px solid #0880AE;
    box-sizing: border-box;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    border-radius: 6px;
}
.inputs, select { 
     width: 100%;
}
input, select {
    height: 52px;
    font-family: IBM Plex Sans;
    padding: 16px;
    background: #FFFFFF;
    border: 1px solid #DBE2EA;
    box-sizing: border-box;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    border-radius: 6px;
}
h4 {
    margin: 0; 
    height: 44px;
    font-family: IBM Plex Sans;
    font-style: normal;
    font-weight: 700;
    font-size: 34px;
    line-height: 44px;
    color: #2C2738;
}
a {
    text-decoration: none;
    color: #0880AE;
}
.card {
    min-width: 342px !important;
    max-width: 500px;
    left: 0%;
    right: 0%;
    top: 0%;
    bottom: 0%;
    margin: 12px auto;
    background: #FFFFFF;
    box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02), 0px 32px 64px rgba(44, 39, 56, 0.04);
    border-radius: 24px;
    padding: 40px 30px;
}
@media (min-width: 600px) {
    .card {
        margin: 28px auto;
    }
}
@media (max-width: 600px) {
    
    .card {
        min-width: 332px !important;
        padding: 18px 12px;
    }
}
</style>