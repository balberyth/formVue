<script setup>
  import { ref } from 'vue';

  let name = ref('');
  let last_name = ref('');
  let dni = ref('');
  let number_dni = ref('');
  let genre = ref('');
  let email = ref('');
  let phone_number = ref('');
  let birth = ref('');

  let show_alert = ref('');
  let show = ref('');
  let a = ref('');

  const alert = (n, msj) => {
    if (n === 1) {
      show_alert.value = msj;
      show.value = 1;
      a.value = 1;
      setTimeout(() => {
        show.value = 0;
      }, 4000);
    } else if (n === 2) {
      show_alert.value = msj;
      show.value = 1;
      a.value = 2;
      setTimeout(() => {
        show.value = 0;
      }, 4000);
    }
  };

  let arr = [];

  const validar = () => {
    const fecha_N = new Date(birth.value);
    const fecha_H = new Date();
    const edad = fecha_H.getFullYear() - fecha_N.getFullYear();

    if (name.value === '') {
      alert(1, 'El nombre está vacío');
    } else if (last_name.value === '') {
      alert(1, 'El apellido está vacío');
    } else if (dni.value === '') {
      alert(1, 'El tipo de documento está vacío');
    } else if (number_dni.value === '') {
      alert(1, 'El número de documento está vacío');
    } else if (isNaN(number_dni.value)) {
      alert(1, 'Ingrese un número de documento válido');
    } else if (genre.value === '') {
      alert(1, 'El género está vacío');
    } else if (email.value === '') {
      alert(1, 'El correo está vacío');
    } else if (!/^([\w!.%+\-])+@([\w\-])+(?:\.[\w\-]+)+$/.test(email.value)) {
      alert(1, 'Ingrese un correo válido');
    } else if (phone_number.value.toString().length < 9) {
      alert(1, 'El número de teléfono debe tener más de 9 dígitos');
    } else if (phone_number.value <= 0) {
      alert(1, 'El número de teléfono debe ser positivo');
    } else if (birth.value === '') {
      alert(1, 'La fecha de nacimiento está vacía');
    } else if (edad < 18) {
      alert(1, 'No se permiten menores de edad');
    } else {
      alert(2, 'Su registro ha sido exitoso');
      arr.push({
        nombre: name.value,
        apellido: last_name.value,
        tipo_de_documento: dni.value,
        numero_de_documento: number_dni.value,
        genero: genre.value,
        correo: email.value,
        telefono: phone_number.value,
        fecha_de_nacimiento: birth.value,
      });
      console.log(arr);
    }
  };
</script>

<template>
  <div>
    <div role="alert" :class="a === 1 ? 'alert-red' : 'alert-aquamarine'" v-show="show === 1">
      <h1>{{ show_alert }}</h1>
    </div>
    <section>
      <input type="text" v-model="name" placeholder="Nombre...">
      <input type="text" v-model="last_name" placeholder="Apellido...">
      <label for="td" class="form-label">Tipo de documento...</label>
      <select v-model="dni" id="td" class="form-select">
        <option value="CC">Cédula de Ciudadanía</option>
        <option value="CE">Cédula Extranjera</option>
        <option value="P">Pasaporte</option>
        <option value="O">Otro</option>
      </select>
      <input type="text" v-model="number_dni" placeholder="Número de documento...">
      <label for="gn" class="form-label">Género...</label>
      <select v-model="genre" id="gn" class="form-select">
        <option value="H">Hombre</option>
        <option value="M">Mujer</option>
        <option value="NN">No sabe, no responde</option>
      </select>
      <input type="email" v-model="email" placeholder="Correo...">
      <input type="tel" v-model="phone_number" placeholder="Teléfono...">
      <input type="date" v-model="birth">
    </section>
    <button @click="validar" class="btn-submit">Aceptar</button>
  </div>
</template>

<style scoped>
 section {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

/* Estilo de las etiquetas del formulario */
label {
  display: block;
  margin-bottom: 8px;
  color: #333;
}

/* Estilo de los campos de entrada */
input[type="text"],
input[type="email"],
input[type="tel"],
input[type="date"],
select {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}

/* Estilo del botón de envío */
.btn-submit {
  background-color: #4caf50;
  color: #fff;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Estilo del botón de envío al pasar el ratón */
.btn-submit:hover {
  background-color: #45a049;
}

/* Estilo del mensaje de alerta */
.alert-red {
  color: #d9534f;
}
</style>