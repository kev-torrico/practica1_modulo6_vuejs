<template>
  <div class="container mt-4">
    <h1 class="mb-4">Editar Contacto</h1>
    <form @submit.prevent="emitirDatosEditados" novalidate>
      <div class="mb-3">
        <label class="form-label d-block w-100 text-start">Name</label>
        <input
          type="text"
          v-model="editado.name"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label class="form-label d-block w-100 text-start">Email</label>
        <input type="email" v-model="editado.email" class="form-control" />
      </div>
      <div class="mb-3">
        <label class="form-label d-block w-100 text-start">Address</label>
        <input
          type="text"
          v-model="editado.address"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label class="form-label d-block w-100 text-start">Phone</label>
        <input
          type="text"
          v-model="editado.phone"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label class="form-label d-block w-100 text-start">Country</label>
        <input
          type="text"
          v-model="editado.country"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label class="form-label d-block w-100 text-start">City</label>
        <input
          type="text"
          v-model="editado.city"
          class="form-control"
          required
        />
      </div>
      <button type="submit" class="btn btn-primary">Guardar</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "ContactoEditar",
  props: {
    contacto: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      editado: { ...this.contacto },
    };
  },
  methods: {
    emitirDatosEditados() {
      this.$emit("update", this.editado);
    },
  },
};
</script>
