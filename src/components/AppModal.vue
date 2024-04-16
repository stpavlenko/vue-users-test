<script>
export default {
  name: 'AppModal',
  props: {
    visible: Boolean,
    flatUsers: Array,
  },
  data () {
    return {
      newUser: {
        name: null,
        phone: null,
        parentId: null,
        id: null,
        children: [],
      },
    }
  },
  methods: {
    close () {
      this.$emit('close')
      this.cleanForm()
    },
    submit () {
      this.$emit('submit', this.newUser)
      this.close()
    },
    cleanForm () {
      this.newUser = {
        name: null,
        phone: null,
        parentId: null,
        id: null,
        children: [],
      }
    },
  },
  computed: {
    isFormValid () {
      return this.newUser.name &&
        this.newUser.phone
    },
  },
}
</script>

<template>
  <div v-show="visible" @click.self="close" class="modal">
    <div class="modal__content card">
      <div class="card__header">
        <strong>Добавление пользователя</strong>
        <button @click="close"><img src="../assets/icons/close.svg"></button>
      </div>

      <form @submit.prevent="submit">
        <label>
          <span>Имя</span>
          <input v-model="newUser.name" type="text" required>
        </label>

        <label>
          <span>Телефон</span>
          <input v-model="newUser.phone" type="tel" required>
        </label>

        <label>
          <span>Начальник</span>
          <select v-model="newUser.parentId">
            <option v-for="user in flatUsers" :key="user.id" :value="user.id">{{ user.name }}</option>
          </select>
        </label>

        <button :disabled="!isFormValid" type="submit">
          Сохранить
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, .4);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal__content {
  flex-grow: 1;
  background: white;
  max-width: 30rem;
  margin: 0.5rem;
}

.card {
  border-radius: .5rem;
  padding: 1rem;
}

.card__header {
  display: flex;
  justify-content: space-between;
}

form {
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;

}

label {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}
</style>
