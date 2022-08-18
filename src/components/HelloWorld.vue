<template>
  <div>
    <h1>{{ name || "Tarefas" }}</h1>
    <h2 v-html="subtitle"></h2>
    <button @click="insert = !insert" class="mb-2">Criar</button>
    <div v-show="insert">
      <strong>Nome da Tarefa :</strong>
      <input
        type="text"
        @keyup.enter="items.push({ ...newItem })"
        v-model="newItem.task"
      />

      <div>
        <strong>Está Completa? :</strong>

        <label>
          <input type="radio" v-model="newItem.completa" value='true' />sim
        </label>

        <label>
          <input type="radio" v-model="newItem.completa" value='false' />não
        </label>
      </div>
      <button
        :disable="newItem.task.length < 3"
        @click="items.push({ ...newItem })"
      >
        Salvar item
      </button>

      <h3>
        items
        <span v-show="items.length > 0">{{ items.length }}</span>
      </h3>

      <p v-if="items.length === 0">Não há items</p>
      <div v-else-if="items.length === 1">1 item</div>
      <span v-else>{{ items.length }} items</span>

      <ul>
        <li v-for="(item, index) in items" :key="item.completa">
          {{ index }}
          <p v-bind:style= "[item.completa=='false' ? {'color': 'red'} : {'color': 'green'}]">{{ item.task }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "Lista de Tarefas",
      subtitle: '<span style="color: green;">Crie uma nova tarefa</span>',
      insert: false,
      items: [],
      newItem: {
        task: "",
        completa: 'false',
      },
    };
  },
};
</script>
