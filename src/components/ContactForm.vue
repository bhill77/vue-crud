<template>
  <div :class="modalClass">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">{{ title }}</p>
        <button class="delete" aria-label="close" @click="onClose"></button>
      </header>
      <section class="modal-card-body">
        <div class="field is-horizontal">
          <div class="field-label is-normal">
            <label class="label">Name</label>
          </div>
          <div class="field-body">
            <div class="field">
              <p class="control">
                <input
                  class="input"
                  type="text"
                  placeholder="Name"
                  v-model="contact.name"
                />
              </p>
            </div>
          </div>
        </div>

        <div class="field is-horizontal">
          <div class="field-label is-normal">
            <label class="label">Email</label>
          </div>
          <div class="field-body">
            <div class="field">
              <p class="control">
                <input class="input" type="text" placeholder="Email" v-model="contact.email">
              </p>
            </div>
          </div>
        </div>

        <div class="field is-horizontal">
          <div class="field-label is-normal">
            <label class="label">Phone</label>
          </div>
          <div class="field-body">
            <div class="field">
              <p class="control">
                <input class="input" type="text" placeholder="Phone" v-model="contact.phone">
              </p>
            </div>
          </div>
        </div>
      </section>
      <footer class="modal-card-foot">
        <button class="button is-success" @click="save">Save</button>
        <button class="button" @click="onClose">Cancel</button>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: 'contact-form',
  props: ['title', 'contact', 'isActive', 'onClose', 'onSave'],
  data() {
    return { name: this.contact.name, email: this.contact.email, phone: this.contact.phone }
  },

  computed: {
    modalClass() {
      return { modal:true, 'is-active': this.isActive }
    },
  },

  methods: {
    save() {
      const data = { name: this.name, email: this.email, phone: this.phone }
      this.onSave(data)
    }
  }
}
</script>

