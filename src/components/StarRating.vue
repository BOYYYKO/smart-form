<template>
    <div>
        <h2>RATE US</h2>
        <div class="star-rating">
            <span v-on:click="setRating(index)" v-for="index in starLimit" :key="index"
                class="star star--outlined"></span>
            <div class="star-rating__colored" :style="ratingWidthStyle">
                <span v-on:click="setRating(index)" v-for="index in starLimit" :key="index"
                    class="star star--colored"></span>
            </div>
        </div>
        <h3>{{ rating }} of 5</h3>
    </div>
</template>

<script>

export default {
    name: 'StarRating',
    props: {
        starLimit: {
            type: Number,
            default: 5
        }
    },
    data() {
      return {
        rating: 0
      }
    },
    computed: {
        ratingWidth() {
            return this.rating / this.starLimit * 100
        },
        ratingWidthStyle() {
            return `width: ${this.ratingWidth}%;`
        }
    },
    methods: {
        setRating(value) {
            this.rating = value;
        }
    }

}
</script>

<style scoped>
.star-rating {
    position: relative;
    display: inline-flex;
}

.star-rating__colored {
    display: inline-flex;
    position: absolute;
    width: 0;
    height: 100%;
    top: 0;
    left: 0;
    overflow: hidden;
}

.star {
    display: inline-block;
    width: 16px;
    height: 16px;
    margin: 0 3px;
    flex-shrink: 0;
}

.star--colored {
    background: url('../img/star.png') center no-repeat;
}

.star--outlined {
    background: url('../img/star2.png') center no-repeat;
}
</style>