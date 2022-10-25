<template>
  <div class="home" @click.self="openModal(null)">
    <slot />
    <ul class="list">
      <li
        class="item"
        v-for="item in list"
        :key="item.id"
        @click.prevent="openModal(item.id)"
      >
        <label class="grid-cell">
          {{ item.name }}
        </label>
        <label class="grid-cell">{{ item.surname }}</label>
        <div class="modal" v-if="selectedLine.id === item.id">
          {{ selectedLine.info }}
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        {
          id: 0,
          name: "Leanne",
          surname: "Graham",
        },
        {
          id: 1,
          name: "Ervin",
          surname: "Howell",
        },
        {
          id: 2,
          name: "Clementine",
          surname: "Bauch",
        },
        {
          id: 3,
          name: "Patricia",
          surname: "Lebsack",
        },
        {
          id: 4,
          name: "Chelsey",
          surname: "Dietrich",
        },
      ],
      selectedLine: {
        id: null,
        info: null,
      },
    };
  },

  methods: {
    openModal(id) {
      this.selectedLine.id = id;
      this.selectedLine.info = `ID - ${id}`;
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  padding: 2em;
  display: flex;
  flex-direction: column;
  gap: 4em;
}

.list {
  padding: 0;
  margin: 0;
  width: 500px;
  display: flex;
  flex-direction: column;
  .item {
    display: grid;
    grid-template-columns: 1fr 2fr;
    place-items: end;
    position: relative;
    .modal {
      position: absolute;
      left: -30px;
      top: 90%;
      z-index: 2;
      padding: 0.5em;
      min-width: 5em;
      width: min-content;
      min-height: 70%;
      height: min-content;
      background-color: #f4f4f4;
      border-radius: 0.5em;
      border: 2px solid #2c3e50;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .grid-cell {
      border: 1px solid #c4c4c4;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      padding: 10px;
    }
  }
}
</style>
