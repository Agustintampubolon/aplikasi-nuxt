<template>
  <div class="py-4">
    <div class="container">
      <div
        class="title border-bottom d-flex align-items-center justify-content-between py-2"
      >
        <h5>Task</h5>

        <div class="d-flex align-items-center ms-auto">
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />

          <div class="d-flex align-items-center">
            <span class="me-2">View As &nbsp;</span>
            <button
              class="btn btn-secondary py-1 px-3"
              @click="isGrid = !isGrid"
            >
              {{ isGrid ? "Grid" : "List" }}
            </button>
          </div>
        </div>
      </div>

      <div class="list-task row">
        <CardItem
          v-for="(task, i) in resultQuery"
          :key="i"
          :task="task"
          :isGrid="isGrid"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },

  data() {
    return {
      searchQuery: "",

      isCreating: false,

      isGrid: false,

      isHidden: false,

      tasks: [
        {
          title: "Lemper",
          description: "Lemper Enak",
          isDone: false,
          category: "Makanan",
          isHidden: false,
        },
        {
          title: "Teh Bohai",
          description: "Teh Bohai Seger",
          isDone: false,
          category: "Minuman",
          isHidden: false,
        },
        {
          title: "Mintz",
          description: "Mintz Seger",
          isDone: false,
          category: "Permen",
          isHidden: false,
        },
        {
          title: "Jagung",
          description: "Jagung Di Bakar",
          isDone: false,
          category: "Makanan",
          isHidden: false,
        },
        {
          title: "Cincau",
          description: "Cincau Bikin Lengket",
          isDone: false,
          category: "Minuman",
          isHidden: false,
        },
        {
          title: "Kopiko",
          description: "Kopiko Adem",
          isDone: false,
          category: "Permen",
          isHidden: false,
        },
      ],
    };
  },

  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else if (this.selected) {
        return this.tasks.filter((item) => {
          return this.selected
            .toLowerCase()
            .split(" ")
            .every((v) => item.category.toLowerCase().includes(v));
        });
      } else {
        console.log(this.tasks);
        return this.tasks;
      }
    },
  },
};
</script>

<style></style>
