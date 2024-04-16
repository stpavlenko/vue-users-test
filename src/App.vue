<script>
import { testUsers } from './assets/testUsers'
import AppModal from './components/AppModal.vue'
import TableRow from './components/TableRow.vue'
import TableHeader from './components/TableHeader.vue'

export default {
  name: 'Users',
  components: { TableHeader, TableRow, AppModal },
  data () {
    return {
      users: [],
      isUserModalVisible: false,
    }
  },
  methods: {
    getFlatUsers (users) {
      let allUsers = []

      users.forEach(user => {
        allUsers.push(user)
        if (user.children.length) {
          allUsers = allUsers.concat(this.getFlatUsers(user.children))
        }
      })
      return allUsers
    },

    findUserById (id, usersArray = this.users) {
      const foundUser = usersArray.find(user => user.id === id)
      if (foundUser) return foundUser

      for (const user of usersArray) {
        const foundInChildren = this.findUserById(id, user.children)
        if (foundInChildren) return foundInChildren
      }
      return null
    },

    saveUsersToLocalStorage () {
      localStorage.setItem('users', JSON.stringify(this.users))
    },

    toggleUserModal () {
      this.isUserModalVisible = !this.isUserModalVisible
    },

    addUser (newUser) {
      newUser.id = Date.now().toString()

      if (newUser.parentId) {
        this.findUserById(newUser.parentId).children.push(newUser)
      } else {
        this.users.push(newUser)
      }

      this.saveUsersToLocalStorage()
    },

    sort (users = this.users) {
      users.sort((a, b) => a.name.localeCompare(b.name))

      users.forEach(user => {
        if (user.children.length) this.sort(user.children)
      })

      this.saveUsersToLocalStorage()
    },

  },
  computed: {
    flatUsers () {
      return this.getFlatUsers(this.users)
    },
  },
  created () {
    this.users = JSON.parse(localStorage.getItem('users')) || testUsers
  },
}
</script>

<template>
  <div class="users">
    <button @click="toggleUserModal">Добавить</button>

    <ul>
      <table-header @sort="sort" />
      <table-row v-for="user in users" :key="user.id" :user="user" :depth="1" />
    </ul>

    <app-modal :visible="isUserModalVisible" :flatUsers="flatUsers" @close="toggleUserModal" @submit="addUser" />
  </div>
</template>

<style scoped>
ul {
  margin-top: 1rem;
}

li {
  padding-left: 0;
}

.users {
  padding-inline: 1rem;
  margin-top: 1rem;
  max-width: 800px;
  margin-inline: auto;
}
</style>
