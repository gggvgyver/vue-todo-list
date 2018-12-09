<template>
  <div>
    <v-card
      class="pa-3 mb-3"
      :class="{ done: list.status === 'done' }"
      v-for="(list, index) in todoList"
      :key="index"
    >
      <p>{{ list.memo }}</p>
      <v-btn
        v-if="list.status === 'created'"
        fab
        flat
        small
        color="green"
        @click="$emit('statusControl', index, 'done')"
      >
        <i class="fas fa-check-circle"></i>
      </v-btn>
      <v-btn
        v-else
        fab
        flat
        small
        color="blue"
        @click="$emit('statusControl', index, 'created')"
      >
        <i class="fas fa-redo-alt"></i>
      </v-btn>
      <v-btn
        v-if="list.status === 'created'"
        @click="listEdit(list.memo, index)"
        fab
        flat
        small
        color="grey"
      >
        <i class="fas fa-edit"></i>
      </v-btn>
      <v-btn @click="$emit('listDelete', index)" fab flat small color="red">
        <i class="fas fa-trash-alt"></i>
      </v-btn>
    </v-card>
  </div>
</template>

<script>
import { eventBus } from "@/main";
export default {
  props: ["todoList"],
  methods: {
    listEdit(memo, index) {
      eventBus.listEdit(memo, index);
    }
  }
};
</script>

<style scoped>
.done {
  background-color: aquamarine;
}
.done p {
  text-decoration: line-through;
  color: blueviolet;
}
</style>
