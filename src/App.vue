<template>
  <main-screen v-if="statusMatch === 'default'"
               @onStart="onHandleBeforeStart($event)" />
  <interact-screen v-if="statusMatch === 'match'"
                   :cardsContext="settings.cardsContext"
                   @onFinish="onGetResult"
          />
  <result-screen :timer="timer"
                 v-if="statusMatch === 'result'"
                 @onStartAgain="statusMatch = 'default'"/>
  <copy-right />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import CopyRight from "./components/Common/CopyRight.vue";

import {shuffled} from "./utils/array";
export default {
  name: 'App',
    components: {
        MainScreen,
        InteractScreen,
        ResultScreen,
        CopyRight
    },
    data() {
      return {
          settings:{
              totalOfBlock: 0,
              cardsContext: [],
              startedAt: null
          },
          statusMatch: "default",
          timer: 0
      }
    },
    methods: {
      onHandleBeforeStart(config) {
          this.settings.totalOfBlock = config.totalOfBlocks;
          const firstCards = Array.from({length: this.settings.totalOfBlock / 2}, (_, i) => i + 1);
          const secondCards = [...firstCards];
          const cards = [...firstCards, ...secondCards];
          this.settings.cardsContext =  shuffled(shuffled(cards));
          this.settings.startedAt = new Date().getTime();

          //data ready
        this.statusMatch = 'match';
      },
        onGetResult(){
          //get timer
            this.timer  = new Date().getTime() - this.settings.startedAt;
            //switch
            this.statusMatch = "result";
        }

    }
}
</script>