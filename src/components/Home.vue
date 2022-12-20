<template>
<div>
    <div id="home" v-if="((!start)&&(!rules))">
        <div id="title">
            <h1>Sex is<span style="color: #A91079;"><br> Strange</span></h1>
        <div class="ovale"></div>
        </div>
        <div id="btn_home_contain">
            <button class="btn_home btn1" v-on:click="demarrer()">Jouer</button>
            <button class="btn_home btn2" v-on:click="openRules()">But du jeu</button>
        </div>
    </div>
    <div class="center">
        <div id="rules" v-if="rules">
            <div id="rulesMessage" v-bind:innerHTML="rulesMessage"></div>
            <button class="rules_btn btn2" v-on:click="closeRules()">Accueil</button>
        </div>
    </div>
</div>

</template>

<script>
import api from '../API/api.json'
export default{
    data(){
        return{
            rules: false,
            rulesMessage: "",
        }
    },
    props:{
        start: Boolean,
    },
    methods:{
        demarrer(){
            this.$emit('demarrer');
        },
        openRules(){
            this.rules = true;
            const message = api.about_game;
            this.rulesMessage = this.nl2br(message, "\n");
        },
        nl2br (str, is_xhtml) {
            var breakTag = (is_xhtml || typeof is_xhtml === 'undefined') ? '<br>' : '<br>';
            return (str + '').replace(/([^>\r\n]?)(\r\n|\n\r|\r|\n)/g, '$1' + breakTag + '$2');
        },
        closeRules(){
            this.rules = false;
        },
    },
}

</script>