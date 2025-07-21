<template>
  <div class="table-container">
    <h2>Agenda de contactos</h2>

    <button class="btn-nuevo-contacto" @click="goToNew()">
      Nuevo Contacto
    </button>

    <table class="user-table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Address</th>
          <th>Phone</th>
          <th>Country</th>
          <th>City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="item.id">
          <th scope="row">{{ item.id }}</th>
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.address }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.country }}</td>
          <td>{{ item.city }}</td>
          <td>
            <button
              type="button"
              class="btn-nuevo-contacto"
              @click="abrirModal(index)"
            >
              Editar
            </button>
            <button
              type="button"
              class="btn btn-danger"
              @click="eliminar(index)"
            >
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- Modal -->
  <div
    class="modal fade"
    id="modalContactoEditar"
    tabindex="-1"
    aria-labelledby="modalContactoEditarLabel"
    aria-hidden="true"
    ref="modalRef"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="modalContactoEditarLabel">
            Editar contacto
          </h1>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <ContactoEditar
            v-if="contactoSeleccionado"
            :contacto="contactoSeleccionado"
            @update="guardarEdicion"
            @cancelar="cerrarModal"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ContactoEditar from "@/components/ContactoEditor.vue";
export default {
  name: "Contactos",
  data() {
    return {
      title: "Contacto",
      items: [
        {
          id: 1,
          name: "Alice Johnson",
          email: "alice.johnson@example.com",
          address: "123 Maple Street",
          phone: "123-456-7890",
          country: "USA",
          city: "New York",
        },
        {
          id: 2,
          name: "Bob Smith",
          email: "bob.smith@example.com",
          address: "456 Oak Avenue",
          phone: "987-654-3210",
          country: "Canada",
          city: "Toronto",
        },
        {
          id: 3,
          name: "Carol White",
          email: "carol.white@example.com",
          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London",
        },
        {
          id: 4,
          name: "David Brown",
          email: "david.brown@example.com",
          address: "321 Elm Street",
          phone: "444-555-6666",
          country: "Australia",
          city: "Sydney",
        },
        {
          id: 5,
          name: "Emily Davis",
          email: "emily.davis@example.com",
          address: "654 Spruce Lane",
          phone: "333-444-5555",
          country: "USA",
          city: "Los Angeles",
        },
      ],
      modalBootstrapInstance: null,
      contactoSeleccionado: null,
      indiceSeleccionado: 0,
    };
  },
  components: {
    ContactoEditar,
  },
  mounted() {
    this.$nextTick(() => {
      if (this.$refs.modalRef) {
        this.modalBootstrapInstance = new bootstrap.Modal(this.$refs.modalRef);
      } else {
        console.error("No se encontro el ref modalRef");
      }
    });
  },
  methods: {
    goToNew() {
      this.$router.push("/create");
    },
    abrirModal(index) {
      this.contactoSeleccionado = null;
      this.indiceSeleccionado = index;
      setTimeout(() => {
        if (this.modalBootstrapInstance) {
          this.modalBootstrapInstance.show();
          this.contactoSeleccionado = { ...this.items[index] };
        } else {
          console.error("modalBootstrapInstance no esta inicializado");
        }
      });
    },
    cerrarModal() {
      if (this.modalBootstrapInstance) {
        this.modalBootstrapInstance.hide();
      }
    },
    guardarEdicion(contactoEditado) {
      console.log("Contacto Editado", contactoEditado);
      this.items[this.indiceSeleccionado] = contactoEditado;
      this.cerrarModal();
    },
    eliminar(index) {
      if (confirm("¿Estas seguro de eliminar este UTO?")) {
        this.items.splice(index, 1);
      }
    },
  },
};
</script>

<style scoped>
.table-container {
  max-width: 100%;
  padding: 1rem;
  background-color: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.user-table {
  width: 100%;
  border-collapse: collapse;
  font-family: Arial, sans-serif;
  background-color: #fff;
}

.user-table th,
.user-table td {
  border: 1px solid #ddd;
  padding: 0.75rem;
  text-align: left;
}

.user-table thead {
  background-color: #293429;
  color: white;
}

.user-table tr:nth-child(even) {
  background-color: #f2f2f2;
}
.btn-nuevo-contacto {
  margin-bottom: 1rem;
  background-color: #4caf50;
  color: white;
  padding: 0.6rem 1rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.btn-nuevo-contacto:hover {
  background-color: #45a049;
}
</style>
