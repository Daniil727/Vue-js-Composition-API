<template>
  <div class="notes">
    <div class="titleOfNotes has-text-centered animationTitleOfNotes">
      <h1>My notes</h1>
    </div>

    <form class="mb-5" @submit.prevent="addNotes">
      <div class="field has-addons-centered has-addons">
        <div class="control">
          <input v-model="newNotesCont" class="input has-background-dark" type="text" placeholder="Find a repository" />
        </div>
        <div class="control">
          <button :disabled="!newNotesCont" class="button is-info">Search</button>
        </div>
      </div>
    </form>

    <div v-for="list in lists" :key="list.id" class="card mb-5 has-background-dark animationCard">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column is-left">
              {{ list.content }}
            </div>
            <div class="column is-2 is-text-right">
              <div class="lineBreaksBtn">
                <div>
                  <button class="button is-info">&#10004;</button>
                </div>
                <div>
                  <button class="button is-danger mt-2">&#9932;</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { v4 as uuidv4 } from 'uuid';

const lists = ref([
  // {
  //   id: "id1",
  //   content: "lorem",
  //   done: true,
  // },
  // {
  //   id: "id2",
  //   content: "content2",
  //   done: true,
  // },
  // {
  //   id: "id3",
  //   content: "content3",
  //   done: true,
  // },
  // {
  //   id: "id4",
  //   content: "content4",
  //   done: true,
  // },
]);

const addNotes = () => {
  const newNotes = {
    id: uuidv4(),
    content: newNotesCont.value,
    done: true,
  };
  lists.value.unshift(newNotes);
  newNotesCont.value = '';
};

const newNotesCont = ref("");


</script>

<style>
@import "bulma/css/bulma.min.css";

.notes {
  margin: 0 auto;
  max-width: 900px;
  padding: 10px;
}

.titleOfNotes {
  padding: 10px;
}

.lineBreaksBtn {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.animationTitleOfNotes{
  -webkit-animation: text-focus-in 1s cubic-bezier(0.550, 0.085, 0.680, 0.530) both;
	        animation: text-focus-in 1s cubic-bezier(0.550, 0.085, 0.680, 0.530) both;
}


.animationCard{
  -webkit-animation: slide-in-blurred-top 0.6s cubic-bezier(0.230, 1.000, 0.320, 1.000) both;
	        animation: slide-in-blurred-top 0.6s cubic-bezier(0.230, 1.000, 0.320, 1.000) both;
}

 @-webkit-keyframes text-focus-in {
  0% {
    -webkit-filter: blur(12px);
            filter: blur(12px);
    opacity: 0;
  }
  100% {
    -webkit-filter: blur(0px);
            filter: blur(0px);
    opacity: 1;
  }
}
@keyframes text-focus-in {
  0% {
    -webkit-filter: blur(12px);
            filter: blur(12px);
    opacity: 0;
  }
  100% {
    -webkit-filter: blur(0px);
            filter: blur(0px);
    opacity: 1;
  }
}

 @-webkit-keyframes slide-in-blurred-top {
  0% {
    -webkit-transform: translateY(-1000px) scaleY(2.5) scaleX(0.2);
            transform: translateY(-1000px) scaleY(2.5) scaleX(0.2);
    -webkit-transform-origin: 50% 0%;
            transform-origin: 50% 0%;
    -webkit-filter: blur(40px);
            filter: blur(40px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateY(0) scaleY(1) scaleX(1);
            transform: translateY(0) scaleY(1) scaleX(1);
    -webkit-transform-origin: 50% 50%;
            transform-origin: 50% 50%;
    -webkit-filter: blur(0);
            filter: blur(0);
    opacity: 1;
  }
}
@keyframes slide-in-blurred-top {
  0% {
    -webkit-transform: translateY(-1000px) scaleY(2.5) scaleX(0.2);
            transform: translateY(-1000px) scaleY(2.5) scaleX(0.2);
    -webkit-transform-origin: 50% 0%;
            transform-origin: 50% 0%;
    -webkit-filter: blur(40px);
            filter: blur(40px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateY(0) scaleY(1) scaleX(1);
            transform: translateY(0) scaleY(1) scaleX(1);
    -webkit-transform-origin: 50% 50%;
            transform-origin: 50% 50%;
    -webkit-filter: blur(0);
            filter: blur(0);
    opacity: 1;
  }
}

</style>
