<template>
    <div name="container">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css">
        <link rel="stylesheet" href="stylesheet.css">
        <!-- Lesson Plans Division-->
            <div id="lessonDisplayDiv">
                <!-- Sort removed for simplicity sake -->
                <!-- Displaying Lessons individually -->
                <div id="lessonBlock" v-for="lesson in lessons" :key="lesson.id" >
                    <div v-if="lesson.showLesson">
                        <!-- lesson information -->
                        <img class="lessonimg" v-bind:src="lesson.image">
                        <div id="infoContainer">
                            <span class= "lessonInfo" id="lessonInfoSub" v-text="lesson.Subject"></span>
                            <span class= "lessonInfo">Location: <span v-text="lesson.Location"></span></span>
                            <span class= "lessonInfo">Price : <span v-text="lesson.price"></span></span>
                        
                            <!-- product count message-->
                            <span class="lessonInfo" v-if="canAddTocart(lesson) == false ">
                                All Spaces Booked!
                            </span>
                            <!-- only less than 3 left -->
                            <span class="lessonInfo" v-else>Spaces: {{lesson.spaces}} </span>

                        </div>
                        <!-- Cart Button -->
                        <button class="addToCartButton" v-if="canAddTocart(lesson)" @click="addl(lesson)">
                            <span class="fas fa-cart-plus"></span> Add To Cart
                        </button>
                        <button class="addToCartButton" v-else disabled>
                            Add To Cart
                        </button>
                    </div>
                </div>
            </div>
        </div>
</template>
<script>
export default {
  name: "ProductList",
  data() {
    return {
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
    };
  },
  methods: {
    addl(lesson) {
      console.log("lesson added", lesson.id);
      this.$emit('addP',lesson);
    },
    //Validating whether course can be added to cart
    canAddTocart: function(course) {
        if (course.spaces > 0){
            return true;
        }
        else {
            return false;
        }
    }
  }
}
</script>