<template>
  <div id="app">
    <h1 class="title">Vue CRUD</h1>
    <button class="button is-info" @click="addContact">Add Contact</button>
    <contact-list
      :contacts="contacts"
      :onEdit="editContact"
      :onDelete="deleteContact"
    />

    <contact-form
      :title="formTitle"
      :isActive="formIsActive"
      :onClose="closeForm"
      :onSave="save"
      :contact="currentContact"
    />
  </div>
</template>

<script>
import axios from 'axios'
import Hello from './components/Hello'
import ContactList from './components/ContactList'
import ContactForm from './components/ContactForm'

export default {
  name: 'app',
  components: {
    ContactList,
    ContactForm
  },

  data() {
    return {
      contacts: [],
      currentContact: { name: '', email: '', phone: '' },
      formTitle: '',
      formIsActive: false,
      mode: ''
    }
  },

  methods: {
    getContacts(){
      const config = {
        headers: { Accept: 'application/json' }
      }
      axios.get('http://localhost:8000/api/contact',)
      .then((res)=>{
        this.contacts = res.data
      }).catch((err)=>{
        console.log(err.response)
      })
    },

    save(){
      if(this.mode == 'add')
        this.storeContact()

      else
        this.updateContact()
    },

    addContact() {
      this.formIsActive = true
      this.mode = 'add'
      this.formTitle = 'Add Contact'
      this.currentContact = { name: '', email: '', phone: '' }
    },

    closeForm(){
      this.formIsActive = false
    },

    storeContact() {
      const config = {
        headers: { Accept: 'application/json' }
      }
      axios.post('http://localhost:8000/api/contact', this.currentContact, config)
      .then((res) => {
        this.formIsActive = false
        this.contacts.push(res.data)
      }).catch(err => console.log(err.response))
    },

    editContact(contact) {
      this.currentContact = Object.assign({}, contact)
      this.formIsActive = true
      this.mode = 'edit'
      this.formTitle = 'Edit Contact'
    },

    updateContact(){
      const config = {
        headers: { Accept: 'application/json' }
      }
      const url = `http://localhost:8000/api/contact/${this.currentContact.id}`
      axios.put(url, this.currentContact, config)
      .then((res) => {
        this.formIsActive = false
        this.getContacts()
      }).catch(err => console.log(err.response))
    },

    deleteContact(id) {
      const url = `http://localhost:8000/api/contact/${id}`
      const config = {
        headers: { Accept: 'application/json' }
      }
      axios.delete(url, {}, config)
      .then((res) => {
        this.getContacts()
      }).catch(err => console.log(err.response))
    }
  },

  mounted(){
    this.getContacts()
  }
}
</script>

