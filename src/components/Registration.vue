<template>
    <div>
        <div v-if="!success" class="block_input">
            <div><b>Имя</b></div>
            <div class="input_window_name" v-bind:class="{'active': redName}">
                <input v-model="userName">
            </div>
            <div><b>Пароль</b></div>
            <div class="input_window_pass" v-bind:class="{'active': redPass}">
                <input v-model="pass" type="password">
            </div>
            <div v-if="warning" class="warning" >Неверное имя или пароль</div>
            <div v-if="!success" class="button" @click="buttonSucces()"> Вход </div>
        </div>
        <div v-if="success">
            <div>Вход выполнен!</div>
            <div class="button" @click="buttonBack()"> Назад </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'App',
    data(){
        return{
            userName: "",
            pass: "",
            redName: false,
            redPass: false,
            warning: false,
            success: false
        }
    },
    methods: {
        buttonSucces(){
            this.redWindows(),
            this.validation()
        },
        buttonBack(){
            this.success = false
            this.warning = false
            this.userName = ""
            this.pass = "" 
        },
        redWindows(){
            if(!this.userName ){
                this.redName = true
            } else {
                this.redName = false
            }
            if(!this.pass){
                this.redPass = true 
            } else {
                this.redPass = false
            }
        },
        validation(){
            axios
            .get(`http://localhost:9779/registration`)
            .then(response => {
                if(!this.userName || !this.pass){
                    this.warning = false
                    return
                }
                if(this.userName == response.data.name && this.pass == response.data.password){
                    this.success = true
                } else {
                    this.warning = true
                }
            })
        }
    }
}
</script>

<style>
    .block_input{
        width: 185px;
        margin: 5px auto 5px auto;
        text-align: left;
    }
    .input_window_name{
        border: 3px solid;
        color: black;
        width: 185px;
        margin: 5px auto 5px auto;
    }

    .input_window_pass{
        border: 3px solid;
        color: black;
        width: 185px;
        margin: 5px auto 5px auto;
    }

    .warning{
        position: absolute;
        color: red
    }
    .active{
        color: red;
    }

    .button{
        background-color: rgb(31, 22, 114);
        width: 185px;
        height: 30px;
        cursor: pointer;
        text-align: center;
        border-radius: 50px;
        margin: 30px auto 5px auto;
        color: #fff;
        padding: 10px 0 0 0;
    }

</style>
