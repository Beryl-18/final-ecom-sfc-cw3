<template>
    <div name="template container">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css">
        <link rel="stylesheet" href="stylesheet.css">
        <div id="cartDisplayDiv" >
        
                <h2> Checkout </h2>
                <!-- Lesson list of added lessons -->
                <div v-for='(item, index) in cart' :key="index" id="checkoutLessonsContainer">

                    <div class="checkout-inner">
                        <!-- Lesson Details displayed -->
                            <strong><span v-text="item.Subject" class="checkout-info"></span></strong>
                            <span class="checkout-info">Price Per Lesson: <strong><span v-text="item.price"></span></strong></span>
                            <span class="checkout-info" > Spaces Chosen: <strong><span v-text="item.quantity"></span></strong></span>
                    
                        <!-- Removal Button -->
                        <button @click="removeOneSpace(item)" class="remove-btn">
                            Remove a Space
                        </button>
                    </div>
                </div>

                <!-- Checkout Details of Customer -->
                <div name="checkoutSection" id="checkout-customer-details">
                    <span class="customer-details-inner-item">Full Name : <input type="text" v-model="this.fullName" id="checkoutName"></span>
                    <span class="customer-details-inner-item">Phone Number : <input type="text" v-model="this.phone" id="checkoutNumber"></span>


                    <!-- enable checkout if both full name and phone number are entered without errors, else disable-->
                    <button class="checkout-btn" @click="checkoutConfirm"> Checkout </button> 


                    <!-- display errors for user information -->
                    <span class="error" v-if="checkoutNameErrs"> *please enter a valid name </span> <span v-else></span>
                    <span class="error" v-if="checkoutPhoneErrs"> *please enter a valid phone number </span> <span v-else></span>

                </div>
        </div>
    </div>
</template>

<script>

export default({
    name : 'CheckoutForm',
    props : ['cart'],
    data (){
        return {
            fullName : "",
            phone : "",
        };
    },
    methods: {
        //Function to process Checkout
        checkoutConfirm(){
            alert("Order has been placed for " + this.fullName +". Thank you!");
            //reset cart and refresh the page
            this.cart.splice(0, this.cart.length);
            document.location.reload();
        },
        removeOneSpace(course){
            console.log("event trigger from comp");
            this.$emit('removeSpace', course);
        }
    },
    computed: {
        cartAggregate(){
            let itemcounter = 0;
                if (this.cart.length > 0){
                    for (let i = 0; i < this.cart.length; i++){
                        itemcounter += this.cart[i].quantity;
                    }
                }
            return itemcounter;
        },
        checkoutNameErrs(){

        //check all conditions, if no errors exist, return false. else true;
            let name = this.name;
            let pattern = /^[a-zA-Z ]*$/;

        //check if name passes express test
            if (!pattern.test(name)){
                return true;
            }
            else {
                return false;
                }
        },

        //Validating the Phone number field in Checkout Page
        checkoutPhoneErrs(){

            //Same as checking errors with name, but with numbers only
            let phone = this.phone;
            let pattern = /^([0-9]*)$/;

            // check if pattern passes the expression test
            if (!pattern.test(phone)){
                return true;
            }
            else {
                return false;
            }
            },

    }
})
</script>
