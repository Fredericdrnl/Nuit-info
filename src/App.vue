<template>
  <Home :start="start" @demarrer="demarrer"></Home>
  <Question :start="start" :endOfChapters="endOfChapters" :data="data" :end="end" :chapter_name="chapter_name" @answer="answer" @nextChap="nextChap"></Question>
</template>


<script>
import Home from './components/Home.vue';
import Question from './components/Question.vue';
import api from './API/api.json';
export default {
  data(){
    return{
      start: false,
      id_story: 0,
      id_chapter: 0,
      max_chap: 1,
      chapter_name: null,
      data: null,
      end: false,
      next_end: false,
      endOfChapters : false,
    }
  },
  methods: {
    demarrer(){
      this.start = true;
      this.id_story = 0;
      this.data = api.chapters[this.id_chapter].stories[this.id_story];
      this.chapter_name = api.chapters[this.id_chapter].name;
      this.next_end = api.chapters[this.id_chapter].stories[this.id_story].end;
      this.end = false;
    },
    async answer(param){
      this.id_story = param;
      this.end = this.next_end;
      if (this.end){
        this.data = api.chapters[this.id_chapter].explications[this.id_story];
        return
      }
      this.data = api.chapters[this.id_chapter].stories[this.id_story];
      this.next_end = api.chapters[this.id_chapter].stories[this.id_story].end;
    },
    nextChap(){
      if (this.id_chapter+1<=this.max_chap){
        this.id_chapter += 1;
        this.demarrer();
        console.log(this.data);
      }
      else{
        this.endOfChapters = true;
      }
    }
  },
  components:{
    Home,
    Question,
  }
  }
</script>


<style>

</style>
