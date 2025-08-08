<script>
    /* const axios = require('axios').default;
    axios.get('https://fakestoreapi.com/products'); */
    import axios from 'axios';

    export default {
        data() {
            return {
            items: [],
            conversion: null
            };
        },
        mounted() {
        this.obtenerItems();
        this.obtenerConversion();
        },
        methods: {
            async obtenerItems() {
                try {
                    const response = await axios.get('https://fakestoreapi.com/products');
                    this.items = response.data;
                } catch (error) {
                    console.error("Error al obtener los items:", error);
                }
            },
            async obtenerConversion() {
                try {
                    const response = await fetch('https://pydolarve.org/api/v2/tipo-cambio?currency=usd');
                    const data = await response.json();
                    this.conversion = data.price;
                } catch (error) {
                    console.error(error);
                }
            }
        }
    };
</script>

<template>
    <h1 class="text-center">Tabla</h1>
    <table class="table table-bordered">
        <thead class="table-primary">
            <tr class="text-center">
                <th scope="col" class="textoNegrita">Imagen Referencial</th>
                <th scope="col" class="textoNegrita">T&iacute;tulo</th>
                <th scope="col" class="textoNegrita">Categor&iacute;a</th>
                <th scope="col" class="textoNegrita">Precio $</th>
                <th scope="col" class="textoNegrita">Precio Bs.D</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in items" :key="item.id">
                <td><img :src="item.image" style="width: 100px; height: 100px;"></td>
                <td>{{item.title}}</td>
                <td>{{item.category}}</td>
                <td>{{item.price}}</td>
                <td>{{(item.price * conversion).toFixed(2)}}</td>
            </tr>
        </tbody>
    </table>
</template>