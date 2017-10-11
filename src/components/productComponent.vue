<template>
    <tr v-if="editMode">
        <td>{{product.name}}</td>
        <td>{{product.quantity}}</td>
        <td>{{product.price}}</td>
        <td>
            <button class="btn btn-primary" v-on:click="editModeChange()">Edit</button>
            <button class="btn btn-danger" v-on:click="removeEvent()">Delete</button>
        </td>
    </tr>

    <tr v-else>
        <td><input type="text" class="form-control" placeholder="Наименование продукта"
                   v-model="product.name"/></td>
        <td><input type="text" class="form-control" placeholder="Количество"
                   v-model="product.quantity"/></td>
        <td><input type="text" class="form-contro mb-3" placeholder="Цена"
                   v-model="product.price"/></td>
        <td>
            <button class="btn btn-primary" v-on:click="save()">save</button>
            <button class="btn btn-secondary" v-on:click="cancel()">cancel</button>
        </td>
    </tr>
</template>

<script>
    /* eslint-disable indent */

    export default {
        name: 'ProductComponent',
        props: ['product'],
        data () {
            return {
                editMode: true,
                name: this.product.name,
                quantity: this.product.quantity,
                price: this.product.price
            }
        },
        methods: {
            editModeChange: function () {
                this.editMode = !this.editMode
            },
            cancel: function () {
                this.product.name = this.name
                this.product.quantit = this.quantity
                this.product.price = this.price
                this.editModeChange()
            },
            save: function () {
                this.name = this.product.name
                this.quantity = this.product.quantity
                this.price = this.product.price
                this.editModeChange()
            },
            removeEvent: function () {
                this.$emit('remove', this.product)
            }
        }

    }
</script>
