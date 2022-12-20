<template>
    <div>
        <div v-if="((start)&&(!end)&&(!endOfChapters))">
            <img class="bg_img" v-bind:src="data.src" alt="">
            <div id="question">
                <div id="info_question">
                    <div id="story_name">{{chapter_name}}&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;{{data.name}}</div>
                <p>{{data.content}}</p>
                </div>
                <div id="rep_question">
                    <div id="story_question">{{data.question}}</div>
                    <div class="center_btn">
                    <div id="btn_question">
                        <button class="btn_question" v-on:click="answered(data.answers[0].redirect)">{{data.answers[0].text_button}}</button>
                        <button class="btn_question" v-on:click="answered(data.answers[1].redirect)">{{data.answers[1].text_button}}</button>
                    </div>
                </div>
                </div>
            </div>
        </div>
        <div v-if="((end)&&(!endOfChapters))">
            <img class="bg_img" v-bind:src="data.src" alt="">
            <div id="end_chapter">
                {{data.general_content}}
                <div class="btn_center">
                    <button class="btn_chapter" v-on:click="nextChap()">Chapitre suivant</button>
                </div>
            </div>
        </div>
        <div v-if="endOfChapters">
            <img class="bg_img" v-bind:src="end_img" alt="">
            <div id="end_chapter">
                Félicitation vous avez fini l'aventure !
                <div class="btn_center">
                    <button class="btn_chapter" v-on:click="restart()">Accueil</button>
                </div>
            </div>   
        </div>
    </div>
</template>

<script>
import api from '../API/api.json';
export default {
    data(){
        return{
            end_img: api.end_src,
        }
    },
    props: {
        chapter_name: String,
        data: Object,
        start: Boolean,
        end: Boolean,
        endOfChapters: Boolean,
    },
    methods: {
        answered(param) {
            this.$emit('answer', param);
        },
        nextChap(){
            this.$emit('nextChap');
        },
        restart(){
            location.reload();
        }
    },
}

</script>