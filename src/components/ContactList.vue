<template>
  <table class="table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
        <th>Phone</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="contact in contacts" :key="contact.id">
        <td>{{ contact.name }}</td>
        <td>{{ contact.email }}</td>
        <td>{{ contact.phone }}</td>
        <td>
          <button class="button is-primary" @click="edit(contact)">Edit</button>
          <button class="button is-danger" @click="del(contact.id)">Delete</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'contact-list',
  props: ['contacts', 'onEdit', 'onDelete'],
  methods: {
    edit(contact){
      this.onEdit(contact)
    },
    del(id) {
      this.onDelete(id)
    }
  }
}
</script>
