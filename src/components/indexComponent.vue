<template>
    <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-8">
            <table class="table table-striped">
                <thead>
                <tr>
                    <th>Наименование</th>
                    <th>Количество</th>
                    <th>Цена</th>
                </tr>
                </thead>
                <tbody>
                <component is='product-component'
                           v-for="product in products"
                           :product="product"
                           @remove="removeProduct(product)">
                </component>
                <tr>
                    <td></td>
                    <td></td>
                    <td v-model="products">Итого: {{getTotal()}}</td>
                    <td></td>
                </tr>
                </tbody>
            </table>
            <div class="form-inline">
                <input type="text"
                       class="form-control mb-3"
                       placeholder="Наименование продукта"
                       v-model="newProduct.name"/>
                <input type="text"
                       class="form-control mb-3"
                       placeholder="Колличество"
                       v-model="newProduct.quantity"/>
                <input type="text"
                       class="form-control mb-3"
                       placeholder="Цена"
                       v-model="newProduct.price"/>
                <button class="btn btn-primary mb-3"
                        v-on:click="addNewProduct(newProduct)">
                    Добавить
                </button>
            </div>
        </div>
        <div class="col-md-2"></div>
    </div>

</template>

<script>
    /* eslint-disable indent */
    import ProductComponent from '@/components/productComponent'

    export default {
        components: {ProductComponent},
        name: 'IndexComponent',
        data () {
            return {
                products: [],
                newProduct: {
                    name: '',
                    quantity: '',
                    price: ''
                }
            }
        },
        methods: {
            getTotal: function () {
                let total = 0
                this.products.forEach((item) => {
                    total += parseInt(item.price)
                })
                return total
            },
            addNewProduct: function (newProduct) {
                this.products.push(newProduct)
                this.newProduct = {
                    name: '',
                    quantity: '',
                    price: ''
                }
            },
            removeProduct: function (product) {
                const index = this.products.indexOf(product)
                this.products.splice(index, 1)
            }
        }

    }
</script>
