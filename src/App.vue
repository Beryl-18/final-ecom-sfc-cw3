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

        
            <lesson-list @addP="addtoCart" v-if="checkoutLogic" :lessons="lessons" ></lesson-list>

            <checkout @removeSpace="remove" v-else :cart="cart" ></checkout>

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
            lessons:[{
                "id" : 1,
                "Subject" : 'Mathematics',
                "Location" : 'Qusais',
                "price" : 200.00,
                "image" : 'images/math.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 2,
                "Subject" : 'Biology',
                "Location" : 'Muhaisnah',
                "price" : 180.00,
                "image" : 'images/biology.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 3,
                "Subject" : 'Chemistry',
                "Location" : 'Qusais',
                "price" : 180.00,
                "image" : 'images/chemistry.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 4,
                "Subject" : 'Pottery',
                "Location" : 'Qusais',
                "price" : 150.00,
                "image" : 'images/pottery.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 5,
                "Subject" : 'Cricket',
                "Location" : 'Bur Dubai',
                "price" : 150.00,
                "image" : 'images/cricket.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 6,
                "Subject" : 'Music',
                "Location" : 'Knowledge Park',
                "price" : 420.00,
                "image" : 'images/music.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 7,
                "Subject" : 'Finance',
                "Location" : 'Deira',
                "price" : 425.00,
                "image" : 'images/finance.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 8,
                "Subject" : 'Soccer',
                "Location" : 'Jumeirah',
                "price" : 750.00,
                "image" : 'images/soccer.png',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 9,
                "Subject" : 'Culinary Arts',
                "Location" : 'Qusais',
                "price" : 500.00,
                "image" : 'images/culinary.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            {
                "id" : 10,
                "Subject" : 'French',
                "Location" : 'Al Barsha',
                "price" : 350.00,
                "image" : 'images/french.jpg',
                "spaces": 5,
                "quantity":0,
                "showLesson": true
            },
            ],
            cart: [],
            checkoutLogic : true
        }
    },
    methods:{
        showCheckout() {
            this.checkoutLogic ? this.checkoutLogic = false : this.checkoutLogic = true;
        },
        //Function to push items to cart
        addtoCart(course){
            console.log("accessing root comp")
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
        remove(course){
            //if there's 1 quantity, then remove quantity from cart
            if (course.quantity == 1 ){
                this.cart.splice(this.cart.indexOf(course),1);
                }

            course.quantity = course.quantity - 1;
            course.spaces = course.spaces + 1;
        },

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
    },
}
</script>