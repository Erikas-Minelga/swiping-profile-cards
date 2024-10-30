<script setup>
    import {ref} from 'vue';
    import ProfileCard from './components/ProfileCard.vue';
    import profiles from './profiles';
    import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
    import { faChevronLeft, faChevronRight  } from '@fortawesome/free-solid-svg-icons';

    let count = ref(0);
    let startX = ref(0);
    let endX = ref(0);
    let className = ref("");

    function startDrag(event){
        startX.value = event.changedTouches[0].clientX;
    }

    function endDrag(event){
      endX.value = event.changedTouches[0].clientX;

      if(startX.value > endX.value)
        swipeLeft();

      if(startX.value < endX.value)
        swipeRight();
    }

    function resetClassName(){

      if(className.value === "swiped-left")
      {
        if(count.value === 0)
          count.value = 3;
        else
          count.value--;
      }
      else if(className.value === "swiped-right")
      {
        if(count.value === 3)
          count.value = 0;
        else
          count.value++;
      }

      className.value = "reappeared";
    }

    function swipeLeft(){
      className.value = "swiped-left";
    }

    function swipeRight(){
      className.value = "swiped-right";
    }

</script>

<template>
  <div id="drag-window" @touchstart="startDrag" @touchend="endDrag">
    <div id="card-wrapper" :class="className" @animationend="resetClassName()">
        <ProfileCard :imageSrc="profiles[count].image" :fbLink="profiles[count].fblink" :lILink="profiles[count].lILink" :xLink="profiles[count].xLink" :instaLink="profiles[count].snapLink" :dribLink="profiles[count].dribLink" :followLink="profiles[count].followLink" :messageLink="profiles[count].messageLink" >
          <template v-slot:name>
            {{ profiles[count].name }}
          </template>
          <template v-slot:handle>
            {{ profiles[count].handle }}
          </template>
          <template v-slot:about-copy>
            {{ profiles[count].about }}
          </template>
        </ProfileCard>
    </div>
  </div>

  <div id="controls">
    <button @click="swipeLeft"><FontAwesomeIcon :icon="faChevronLeft"></FontAwesomeIcon></button>
    <button @click="swipeRight"><FontAwesomeIcon :icon="faChevronRight"></FontAwesomeIcon></button>
  </div>
</template>

<style scoped>
  div{
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 50px;
    margin-top: 30px;
    width: 100%;
  }

  @keyframes swipe-left {
    0% {right: 0; bottom: 0; opacity: 1;}
    100% {right: 300px; bottom: 200px; transform: rotate(-190deg); opacity: 0;}
  }

  @keyframes swipe-right {
    0% {left: 0; bottom: 0; opacity: 1;}
    100% {left: 300px; bottom: 200px; transform: rotate(190deg); opacity: 0;}
  }

  @keyframes reappear{
    0% {opacity: 0; transform: scale(0.7); bottom: 95px;}
    50% {opacity: 1; transform: scale(1);}
    100% { bottom: 0;}
  }

  #card-wrapper{
    position: relative;
  }

  .swiped-left{
    animation: swipe-left 0.6s ease-in-out;
  }

  .swiped-right{
    animation: swipe-right 0.6s ease-in-out;
  }

  .reappeared{
    animation: reappear 0.6s ease-in-out;
  }

  #controls > button{
    height: 50px;
    width: 50px;
    font-size: 2rem;
    border-radius: 100%;
    border: 0;
    background-color: #E0408A;
    color: #FFFFFF
  }

  #controls > button:hover{
    cursor: pointer;
  }

  #drag-window{
    width: 100vw;
  }
</style>
