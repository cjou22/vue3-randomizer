<template>
  <div id="app">
    <div class="main">
      <h3>Generate a random list</h3>
      <div>Total: {{ total }}</div>
      <div class="listContainer">
        <textarea
          id="taList"
          rows="20"
          cols="50%"
          v-model="userList"
          placeholder="Enter your list here"
        />
        <textarea id="taListNew" rows="20" cols="50%" v-model="userListNew" />
      </div>
      <div>
      abcd
        <button class="bg-sky-500 hover:bg-sky-700" @click="submitList" id="btnSubmit">Submit</button>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted } from 'vue';

export default {
  name: 'App',
  components: {},
  setup() {
    onMounted(() => {
      console.log('app mounted');
    });
  },
  data() {
    return {
      userList: '',
      userListNew: '',
    };
  },
  methods: {
    submitList() {
      this.userListNew = this.shuffle([...this.userList.split(/[,\n\r]/)])
        .filter((elm) => elm)
        .join('\n');
    },
    // Fisher-Yates (aka Knuth) Shuffle
    shuffle(array) {
      let currentIndex = array.length,
        randomIndex;

      // While there remain elements to shuffle.
      while (currentIndex > 0) {
        // Pick a remaining element.
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        // And swap it with the current element.
        [array[currentIndex], array[randomIndex]] = [
          array[randomIndex],
          array[currentIndex],
        ];
      }

      return array;
    },
  },
  computed: {
    total() {
      return this.userList.split(/[,\n\r]/).length;
    }
  }
  
};
</script>

<style>
#app {
  font-family: system-ui, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 14px;
}

.main {
  width: 80%;
  display: block;
}

.listContainer {
  diplay: inline;
  width: 100%;
}

textarea {
  padding: 10px;
  font-size: 1.1em;
  font-family: 'system-ui', 'sans-serif';
  margin: 10px;
  width: 45%;
}
</style>
