<template>
<div name="app container">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css">
    <link rel="stylesheet" href="stylesheet.css">
    <div id = "lessonplanapp">
            <!-- Navbar -->
            <div id="navbar">
                <!-- Shoppping Cart Button -->
                <div>
                    <button class="checkoutCart" v-if="cartAggregate > 0" @click="showCheckout()">
                        <!-- create logic to switch between checkout and lesson plan? -->
                        Checkout <span class="fas fa-cart-plus"></span> {{cartAggregate}}
                    </button>
                    <button class="checkoutCart" v-else disabled>
                        <!-- create logic to switch between checkout and lesson plan? -->
                         Checkout <span class="fas fa-cart-plus"></span>
                    </button>
                </div>
            </div>

        <main>
            <lesson-list v-if="checkoutLogic" @addLesson="addToCart" ></lesson-list>

            <checkout v-else :cart="cart" ></checkout>
        </main>
    </div>
</div>
</template>

<script>
import lessonList from "./components/lessonList.vue";
import checkout from "./components/Form.vue";

export default {
    name:'App',
    components : {
        lessonList,
        checkout
    },
    data(){
        return{
            cart: [],
            checkoutLogic : true
        }
    },
    methods:{
    //Function to push items to cart
        addtoCart(course){
            let lessonIncart = this.cart.find(i => i.id == course.id);
            if (lessonIncart){
                lessonIncart.quantity++;
                course.spaces = course.spaces - 1;
                }
            else {
                this.cart.push(course);
                course.quantity++;
                course.spaces = course.spaces - 1;
            }
       },
    showCheckout() {
        this.checkoutLogic ? this.checkoutLogic = false : this.checkoutLogic = true;
        }
    },
    computed:{
        cartAggregate(){
            let itemcounter = 0;
                if (this.cart.length > 0){
                    for (let i = 0; i < this.cart.length; i++){
                        itemcounter += this.cart[i].quantity;
                    }
                }
            return itemcounter;
        }
    }
    
}
</script>