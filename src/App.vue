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

    <div v-for="i in 3" :key="i" class="card mb-5">
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div class="column is-left">
              Lorem ipsum leo Lorem ipsum dolor sit amet consectetur adipisicing
              elit. 
            </div>
            <div class="column is-4 is-text-right ">
              <button class="button is-black">&#128504;</button>
              <button class="button is-danger ml-2">&#9932;</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script></script>

<style>
@import "bulma/css/bulma.min.css";

.notes {
  margin: 0 auto;
  max-width: 500px;
  padding: 10px;
}
.titleOfNotes {
  padding: 10px;
}
</style>
