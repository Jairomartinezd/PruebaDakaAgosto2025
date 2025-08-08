<script>
    /* const axios = require('axios').default;
    axios.get('https://fakestoreapi.com/products'); */
    import axios from 'axios';

    export default {
        data() {
            return {
            items: []
            };
        },
        mounted() {
            axios.get('https://fakestoreapi.com/products')
            .then(response => {
                this.items = response.data.results;
            })
            .catch(error => {
                console.error("Hubo un error:", error);
            });
        }
    };
</script>

<template>
    <h1 class="text-center">Tabla</h1>
    <table class="table table-bordered">
        <thead class="table-primary">
            <tr>
                <th scope="col">Imagen Referencial</th>
                <th scope="col">T&iacute;tulo</th>
                <th scope="col">Categor&iacute;a</th>
                <th scope="col">Precio</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in items" :key="item.id">
                <td>{{item.image}}</td>
                <td>{{item.title}}</td>
                <td></td>
                <td></td>
            </tr>
        </tbody>
    </table>
</template>