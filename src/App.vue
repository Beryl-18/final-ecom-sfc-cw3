<template>
<div name="app container">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css">
    <link rel="stylesheet" href="stylesheet.css">
    <div id = "lessonplanapp">
        <main>
            <lesson-list @addLesson="addToCart" ></lesson-list>

            <checkout :cart="cart" ></checkout>
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
            cart: []
        }
    },
    methods:{
        addToCart(){

        }
    }
}
</script>