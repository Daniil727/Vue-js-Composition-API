<template>
  <div class="notes">
    <div class="titleOfNotes has-text-centered">
      <h1>My notes</h1>
    </div>

    <div class="field has-addons-centered has-addons">
      <div class="control">
        <input class="input" type="text" placeholder="Find a repository" />
      </div>
      <div class="control">
        <button class="button is-info">Search</button>
      </div>
    </div>

    <div v-for="list in lists" :key="list.id" class="card mb-5">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column is-left">
              <div class="lineBreaks">
                <div>&#8470;{{ list.number }}</div>
                <div class="mt-2">
                  {{ list.content }}
                </div>
              </div>
            </div>
            <div class="column is-2 is-text-right">
              <div class="lineBreaksBtn">
                <div>
                  <button class="button is-black">&#10004;</button>
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

const lists = ref([
  {
    id: "id1",
    number: "1",
    content: "lorem",
    done: true,
  },
  {
    id: "id2",
    number: "2",
    content: "content2",
    done: true,
  },
  {
    id: "id3",
    number: "3",
    content: "content3",
    done: true,
  },
  {
    id: "id4",
    number: "4",
    content: "content4",
    done: true,
  },
]);
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

.lineBreaks {
  display: flex;
  flex-direction: column;
}

.lineBreaksBtn {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
