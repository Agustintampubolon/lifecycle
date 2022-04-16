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
            <button
              class="btn btn-outline-secondary py-1 px-3"
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

      isGrid: false,

      tasks: [
        {
          title: "Lemper",
          description: "Lemper Enak",
          isDone: false,
          category: "Makanan",
          selected: "",
        },
        {
          title: "Teh Bohai",
          description: "Teh Bohai Seger",
          isDone: false,
          category: "Minuman",
          selected: "",
        },
        {
          title: "Mintz",
          description: "Mintz Seger",
          isDone: false,
          category: "Permen",
          selected: "",
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

  created: function () {
    console.log(this.tasks);
    return this.tasks;
  },

  beforeMount() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start();
      setTimeout(() => this.$nuxt.$loading.finish(), 5000);
    });
  },

  mounted: function () {
    setInterval(() => {
      this.loopTask();
    }, 3000);
  },

  methods: {
    loopTask() {
      console.log(this.tasks);
    },
  },

  computed: {
    resultQuery() {
      if (this.searchQuery != "" && this.searchQuery) {
        return this.tasks.filter((tasks) => {
          return tasks.title
            .toUpperCase()
            .includes(this.searchQuery.toUpperCase());
        });
      } else {
        console.log(this.tasks);
        return this.tasks;
      }
    },
  },
};
</script>

<style>
.my-dropdown-toggle {
  border-radius: 5px;
}
</style>
