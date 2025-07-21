<template>
  <h1>{{ title }}</h1>
  <form class="contact-form" @submit.prevent="submit" novalidate>
    <div class="form-group">
      <label for="name">Name</label>
      <input id="name" v-model="contacto.name" type="text" required />
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input id="email" v-model="contacto.email" type="email" required />
    </div>

    <div class="form-group">
      <label for="address">Address</label>
      <input id="address" v-model="contacto.address" type="text" />
    </div>

    <div class="form-group">
      <label for="phone">Phone</label>
      <input id="phone" v-model="contacto.phone" type="tel" />
    </div>

    <div class="form-group">
      <label for="country">Country</label>
      <input id="country" v-model="contacto.country" type="text" />
    </div>

    <div class="form-group">
      <label for="city">City</label>
      <input id="city" v-model="contacto.city" type="text" />
    </div>

    <button type="submit">Guardar Contacto</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "Nuevo Contacto",
      contacto: {
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: "",
      },
    };
  },
  methods: {
    submit() {
      console.log("Enviando contacto:", this.contacto);
    },
  },
};
</script>

<style scoped>
.contact-form {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  background-color: #fff;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.05);
  max-width: 500px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

label {
  font-weight: bold;
  margin-bottom: 0.5rem;
}

input {
  padding: 0.5rem;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 1rem;
}

button {
  background-color: #4caf50;
  color: white;
  padding: 0.75rem;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: #3e3e3e;
}
</style>
