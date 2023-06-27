<template>
  <div>
    <vue-form :state="formstate" @submit.prevent="onSubmit" class="formulario">
      <div class="form-content">
        <validate tag="label" class="label-form">
          <span>Nombre*</span>
          <input type="text" v-model="model.name" required name="name" />
          <field-messages name="name" show="$touched || $submitted" class="message-required">
            <div slot="required">El nombre es requerido</div>
          </field-messages>
        </validate>
  
        <validate tag="label" class="label-form">
          <span>Email*</span>
          <input type="email" v-model="model.email" name="email" required />
          <field-messages name="email" show="$touched|| $submitted" class="message-required">
            <div slot="required">El email es requerido</div>
            <div slot="email">El email no es válido</div>
          </field-messages>
        </validate>
  
        <validate tag="label" class="label-form">
          <span>Teléfono*</span>
          <input type="tel" v-model="model.phone" name="phone" required pattern="[0-9]{10}" />
          <field-messages name="phone" show="$touched|| $submitted" class="message-required">
            <div slot="required">El teléfono es requerido</div>
            <div slot="pattern">El teléfono debe contener 10 dígitos numéricos</div>
          </field-messages>
        </validate>
  
        <validate tag="label" class="label-form">
          <span>Fecha de nacimiento*</span>
          <input type="date" v-model="model.birthDate" name="birthDate" required />
          <field-messages name="birthDate" show="$touched || $submitted" class="message-required">
            <div slot="required">La fecha de nacimiento es requerida</div>
          </field-messages>
        </validate>
  
        <validate tag="label" class="label-form">
          <span>País de residencia*</span>
          <select v-model="model.country" name="country" required>
            <option value="" disabled selected>Selecciona un país</option>
            <option v-for="country in countries" :value="country" :key="country">{{ country }}</option>
          </select>
          <field-messages name="country" show="$touched || $submitted" class="message-required">
            <div slot="required">El país de residencia es requerido</div>
          </field-messages>
        </validate>
      </div>

      <div class="actions">
        <button type="submit" class="submit-btn">Enviar</button>
        <button class="submit-btn" @click="resetForm">Clear</button>
      </div>
    </vue-form>
  </div>
</template>

<script>
import Swal from "sweetalert2";
export default {
  name: "FormularioComponent",
  data() {
    return {
      formstate: {},
      model: {
        name: "",
        email: "",
        phone: "",
        birthDate: "",
        country: ""
      },
      countries: [
        "Argentina",
        "Brasil",
        "Chile",
        "Colombia",
        "México",
        "Perú",
        "España",
        "Estados Unidos",
        "Otros"
      ]
    };
  },
  methods: {
    onSubmit() {
      if (this.formstate.$valid) {
        Swal.fire({
          title: '¡Formulario enviado!',
          icon: 'success',
          showConfirmButton: false,
          timer: 1500
        });
        this.$emit("datosIngresados", this.model); // Emitir evento con los datos ingresados
        return;
      }
    },
    resetForm() {
      this.model = {
        name: "",
        email: "",
        phone: "",
        birthDate: "",
        country: ""
      };
      this.formstate._reset();
    }
  }
};
</script>

<style scoped>
  .formulario{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 50%;
    margin-left: 25%;
    background: darkcyan;
    border-radius: 10px;
    box-shadow: 3px 3px 4px 4px rgba(0, 0 ,0, 0.1);
    height: 100vh;
    padding: 15px;
    margin-bottom: 60px;
  }

  .actions{
    display: flex;
    align-items: flex-end;
    justify-content: center;
  }

  .submit-btn{
    width: 21%;
    height: 35px;
    border-radius: 10px;
    border: 1px solid greenyellow;
    background: aquamarine;
    text-align: center;
    margin: 10px;
  }
  .label-form{
    display: flex;
    flex-direction: column;
    row-gap: 10px;
    color: white;
    height: auto;
  }
  .message-required{
    color: #bc2323;
    font-weight: 600;
  }
</style>
