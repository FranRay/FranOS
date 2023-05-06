<template>
    <div class="card">
        <div class="card-image" :style="{ backgroundImage: `url(${image})`}">
            <div class="card-title">
                <h2>{{ title }}</h2>
            </div>
        </div>
    </div>
</template>

<script setup lang = "ts">
  const props = defineProps({
    image: {
        type: String,
        required: true,
    },

    title:{
        type: String,
        required: true,
    }
  })
</script>

<style scoped lang = "scss">
    .card {
        display: flex;
        flex-direction: column;
        width: 100%;
        justify-content: center;
        align-items: center;

        .card-image {
            aspect-ratio: 4/3;
            width: 100%;
            height: auto;

            overflow: hidden;
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            border-radius: 1em;

            .card-title {
                opacity: 0;
                display: flex;
                justify-content: center;
                align-items: center;

                width: 100%;
                height: 100%;
                
                background-color: rgba(0, 0, 0, 0.5);
            }

            &:hover .card-title {
                cursor: pointer;
                opacity: 1;
                
            }
        }

        h2 {
            color: white;
            margin-block: 0.25em;
        }
    }

</style>