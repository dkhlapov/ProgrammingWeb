<template>
  <div id="app">
    <nav class="c-nav">
      <ul class="c-nav-list">
        <li class="c-nav-list-item active">
          Home
        </li>

        <li class="c-nav-list-item">
          Voting
        </li>
      </ul>
    </nav>

    <div class="c-alert">
      Something went wrong
    </div>

    <div class="c-alert warning">
      Warning
    </div>

    <div class="c-alert success">
      Success
    </div>

    <h1>
      Eurosong festival
    </h1>

    <p>
      This is our voting application
    </p>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

import style from "./scss/style.scss"

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

