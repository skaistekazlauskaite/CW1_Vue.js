<html>

<head>
<title>Lessons for you</title>
<script src="https://unpkg.com/vue"></script>
<script src="products.js"></script>
</head>

<body>
    <div id="app">
        <header>
            <h1 v-text="sitename"></h1>
            <button v-on:click='showCheckout'>
                {{this.cart.length}}
                <span class="fas fa-cart-plus"></span> Checkout
            </button>
        </header>
        
        <main>
            <div v-if='showProduct'>
                <div v-for='product in products'>
            <figure>
                <img v-bind:src="product.image">
            </figure>
            
            <h2 v-text="product.title"></h2> 
            <p v-text="product.place"></p>
            <p>Price: {{product.price}}</p>
            <p> Number of Spaces: {{product.spaces}}</p>

            <button v-on:click='addToCart(product)' v-if='canAddToCart(product)'>Add to Cart</button>
            <button disabled="disabled" v-else>Add to Cart</button>
            <span v-if='product.spaces === cartCount(product.id)'>All Booked!</span>
            <span v-else-if='product.spaces - cartCount(product.id)
            < 10'>
                Only {{product.spaces - cartCount(product.id)}} left
            </span>
            <span v-else>You can still book it!</span>
                </div>
            </div>
            
            <div v-else>
                <h2>Checkout</h2>
                <p>
                <strong>First Name</strong>
                <input v-model.text='order.firstName'></p>

                <p>
                    <strong>Last Name</strong>
                    <input v-model.text='order.lastName'></p>

                    <p>
                        <strong>Number</strong>
                        <input v-model.number='order.number'></p>
            </div>
        </main>
    </div>

    
    
   
   <script type="text/javascript">
   
    var webstore = new Vue({
        el: '#app',
        data: {
            sitename: 'Lessons for you',
            products : products,
            
            cart:[],
            showProduct: true, 
        },
        methods: {
            addToCart(product) {
                this.cart.push(product.id)
            },
            showCheckout() {
                this.showProduct = this.showProduct ? false : true;
            },
            submitForm() {
                alert('Lesson booked!')
            },
            canAddToCart (product) {
                return product.spaces > this.cartCount(product.id)
            },
            cartCount(id) {
                let count = 0;
                for(let i=0; i<this.cart.length; i++) {
                if (this.cart[i] ===id) count++;
                }
            return count;
            }

        },

        computed: {
            cartItemCount() {
                return this.cart.length;
            },
            canAddToCart() {
                return this.product.spaces > this.cartItemCount;
            }
        },
        
       
    });
        </script>
</body>
</html>
