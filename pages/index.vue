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

          <select
            name="Category"
            class="form-control"
            placeholder="Pilih Kategori"
            v-model="selected"
            :tasks="tasks"
          >
            <option :value="null" selected>-- Select Category --</option>
            <option v-bind:value="tasks[0].category">
              <span> {{ tasks[0].category }} </span>
            </option>
            <option v-bind:value="tasks[1].category">
              <span> {{ tasks[1].category }} </span>
            </option>
            <option v-bind:value="tasks[2].category">
              <span> {{ tasks[2].category }} </span>
            </option>
          </select>

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

      selected: null,

      tasks: [
        {
          title: "Lemper",
          description: "Lemper Enak",
          isDone: false,
          category: "Makanan",
        },
        {
          title: "Teh Bohai",
          description: "Teh Bohai Seger",
          isDone: false,
          category: "Minuman",
        },
        {
          title: "Mintz",
          description: "Mintz Seger",
          isDone: false,
          category: "Permen",
        },
        {
          title: "Jagung",
          description: "Jagung Di Bakar",
          isDone: false,
          category: "Makanan",
        },
        {
          title: "Cincau",
          description: "Cincau Bikin Lengket",
          isDone: false,
          category: "Minuman",
        },
        {
          title: "Kopiko",
          description: "Kopiko Adem",
          isDone: false,
          category: "Permen",
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
