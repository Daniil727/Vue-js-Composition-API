<template>
  <div class="notes">
    <div class="titleOfNotes has-text-centered animationTitleOfNotes">
      <h1>My notes</h1>
    </div>

    <form name="form" action="#" class="mb-5" @submit.prevent="addNotes">
      <div class="field has-addons-centered has-addons">
        <div class="control">
          <input name="input" v-model="newNotesCont" class="input has-background-dark" type="text"
            placeholder="Find a repository" />
        </div>
        <div class="control">
          <button :disabled="!newNotesCont" class="button is-info">
            Search
          </button>
        </div>
      </div>
    </form>

    <div v-for="list in lists" :key="list.id" class="card mb-5 has-background-dark animationCard"
      :class="{ 'has-background-info-dark': list.done }">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column is-left" :class="{ 'has-text-success-light line-through': list.done }">
              {{ list.content }}
            </div>
            <div class="column is-2 is-text-right">
              <div class="lineBreaksBtn">
                <div>
                  <button @click="toggleDone(list.id)" class="button is-info"
                    :class="list.done ? 'is-info' : 'is-dark'">
                    &#10004;
                  </button>
                </div>
                <div>
                  <button @click="deleteNotes(list.id)" class="button is-danger mt-2">
                    &#9932;
                  </button>
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
import { ref, onMounted } from "vue";
import { collection, onSnapshot, addDoc, doc, deleteDoc, updateDoc } from "firebase/firestore";
import { db } from "@/firebase";

const listsCollectionRef = collection(db, "lists")

const lists = ref([
]);

// добавляем данные из firebase

onMounted(() => {
  onSnapshot(listsCollectionRef, (querySnapshot) => {
    const firebaselists = [];
    querySnapshot.forEach((doc) => {
      const list = {
        id: doc.id,
        content: doc.data().content,
        done: doc.data().done,
      };
      firebaselists.push(list);
    });
    lists.value = firebaselists
  });
})

// добавляем данные в firebase

const addNotes = () => {
  addDoc(listsCollectionRef, {
    content: newNotesCont.value,
    done: false,
  });
  newNotesCont.value = "";
};

const newNotesCont = ref("");

//удаление 

const deleteNotes = (id) => {
  deleteDoc(doc(listsCollectionRef, id));
  console.log("id:", id);
};

//отметка о выполнении 

const toggleDone = (id) => {
  const index = lists.value.findIndex((list) => list.id === id);

  // тоблер динамического переключения true/false

  updateDoc(doc(listsCollectionRef, id), {
    done: !lists.value[index].done
  });
};
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

.line-through {
  text-decoration: line-through;
}

.animationTitleOfNotes {
  -webkit-animation: text-focus-in 1s cubic-bezier(0.55, 0.085, 0.68, 0.53) both;
  animation: text-focus-in 1s cubic-bezier(0.55, 0.085, 0.68, 0.53) both;
}

.animationCard {
  -webkit-animation: slide-in-blurred-top 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
  animation: slide-in-blurred-top 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
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
