<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable class="list-index" :list="lists" @end="movingList">
        <List
              v-for="(item, index) in lists"
              :key="item.id"
              :title="item.title"
              :listIndex="index"
              :cards="item.cards"
              @change="movingCard"
              ></List>
        <ListAdd></ListAdd>
      </draggable>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
import ListAdd from './ListAdd.vue';
import List from './List.vue';
import { mapState } from 'vuex'

export default {
  components: {
    ListAdd,
    List,
    draggable
  },
  computed: {
    ...mapState([
      'lists'
    ]),
    totalCardCount() {
      return this.$store.getters.totalCardCount
    }
  },
  methods: {
    movingCard() {
      this.$store.dispatch('updateList', {lists: this.lists})
    },
    movingList() {
      this.$store.dispatch('updateList', {lists: this.lists})
    }
  }
}
</script>
