<template>
    <h1>Registro de Profesores</h1>
    <section class="form-container">
        <form class ="formulario">
            <div>
            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" name="nombre" v-model="profesor.nombre" required />
            </div>
            <div>
            <label for="apellido">Apellido:</label>
            <input type="text" id="apellido" name="apellido" v-model="profesor.apellido" required />
            </div>
            <div>
            <label for="dni">DNI:</label>
            <input type="number" id="dni" name="dni" v-model="profesor.dni" required />
            </div>
            <div>
            <label for="materia">Materias:</label>
            <input type="text" id="materia" name="materia"  v-model="nuevaMateria" />
            <button type="button" class="agregar-materia" v-on:click="agregarMateria">Agregar Materia</button>
            <ul>
                <label v-if="profesor.materias.length > 0">Materias Agregadas:</label>
                <li v-for="(materia, index) in profesor.materias" :key="index">{{ materia }}</li>
            </ul>
            </div>
            <div>
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" v-model="profesor.email" required />
            </div>
            <div>
            <label for="telefono">Teléfono:</label>
            <input type="tel" id="telefono" name="telefono" v-model="profesor.telefono" required />
            </div>
            <div class="documentos">
            <input type="checkbox" v-model="profesor.documentosEntregados" /> Documentos Entregados
            </div>

            <button type="submit" v-on:click="agregarProfesor">Enviar</button>
        </form>
    </section>

    <section class="listado">
        <h3>Listado de Profesores Registrados</h3>
        <table border="1">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>DNI</th>
                    <th>Materias</th>
                    <th>Email</th>
                    <th>Teléfono</th>
                    <th>Documentos Entregados</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(prof, index) in profesores" :key="index">
                    <td>{{ prof.nombre }}</td>
                    <td>{{ prof.apellido }}</td>
                    <td>{{ prof.dni }}</td>
                    <td>
                        <ul>
                            <li v-for="(materia, mIndex) in prof.materias" :key="mIndex">{{ materia }}</li>
                        </ul>
                    </td>
                    <td>{{ prof.email }}</td>
                    <td>{{ prof.telefono }}</td>
                    <td>{{ prof.documentosEntregados ? 'Sí' : 'No' }}</td>
                </tr>
            </tbody>
        </table>
    </section>

</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue';

interface Profesor {
    nombre: string;
    apellido: string;
    dni: string;
    materias: Array<string>;
    email: string;
    telefono: string;
    documentosEntregados: boolean;
}

let profesor: Ref<Profesor> = ref({
    nombre: '',
    apellido: '',
    dni: '',
    materias: [],
    email: '',
    telefono: '',
    documentosEntregados: false
});

let profesores: Ref<Array<Profesor>> = ref([]);

let nuevaMateria: Ref<string> = ref('');

const agregarMateria = () => {
    if (nuevaMateria.value.trim() !== '') {
        profesor.value.materias.push(nuevaMateria.value.trim());
        nuevaMateria.value = '';
    }
};

const agregarProfesor = () => {
    profesores.value.push({ ...profesor.value });
    profesor.value = {
        nombre: '',
        apellido: '',
        dni: '',
        materias: [],
        email: '',
        telefono: '',
        documentosEntregados: false
    };
};

</script>

<style scoped>
.form-container {
    justify-content: left;
    align-items: left;
    float: left ;
    height: 100vh;
    margin-left: 40px;
}
.formulario {
    display: flex;
    flex-direction: column;
    max-width: 400px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
}
.formulario label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    text-align: left;
}
.formulario div {
    margin-bottom: 15px;
}
.formulario input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
    border: 1px solid #ccc;
    border-radius: 4px;
}
.formulario button {
    padding: 10px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
.formulario button:hover {
    background-color: #218838;
}
h1 {
    text-align: left;
    margin-left: 40px;
}
.agregar-materia {
    margin-top: 10px;
}

.documentos {
    display: flex;
    align-items: center;
    gap: 10px;
}

.listado {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-left: 500px;
    padding: 20px;
}
.listado table {
    width: 90%;
    border-collapse: collapse;
    margin-top: 20px;
}
.listado th, .listado td {
    border: 1px solid #ccc;
    padding: 8px;
    text-align: left;
}
.listado th {
    background-color: #f2f2f2;
}
.listado h3 {
    margin-bottom: 10px;
}


</style>
