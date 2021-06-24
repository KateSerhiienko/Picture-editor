<template>
  <div class="container">
    <div class="flex">
      <div class="img-wrapper">
        <img
          v-if="isCatVisible"
          src="../assets/cat.jpeg"
          :style="imgStyles"
          :class="imgFilters"
        >
        <p v-else>The cat will return</p>
      </div>
      <div class="controls">
        <h1>Disgruntled cat</h1>

        <h2>Filters</h2>
        <div class="btn-group flex">
          <button
            type="button"
            :class="imgFilters.sepia ? 'active' : ''"
            @click="imgFilters.sepia = !imgFilters.sepia"
          >
            Sepia
          </button>
          <button
            type="button"
            :class="imgFilters.border ? 'active' : ''"
            @click="imgFilters.border = !imgFilters.border"
          >
            Frame
          </button>
          <button
            type="button"
            :class="{ active: imgFilters.shadow }"
            @click="imgFilters.shadow = !imgFilters.shadow"
          >
            Shadow
          </button>
        </div>

        <h2>Sizes</h2>
        <div class="btn-group flex">
          <label>
            Width: {{ imgSizes.currentWidth }}
            <input
              type="range"
              :value="imgSizes.currentWidth"
              @input="imgSizes.currentWidth = $event.target.value"
              :min="imgSizes.minWidth"
              :max="imgSizes.maxWidth"
          >
          </label>
          <label>
            Height: {{ imgSizes.currentHeight }}
            <input
              type="range"
              :value="imgSizes.currentHeight"
              @input="imgSizes.currentHeight = $event.target.value"
              :min="imgSizes.minHeight"
              :max="imgSizes.maxHeight"
          >
          </label>
        </div>

        <h2>Rotation</h2>
        <div class="btn-group flex">
          <label>
            Angle: {{ imgAngles.currentAngle }}
            <input
              type="range"
              :value="imgAngles.currentAngle"
              @input="imgAngles.currentAngle = $event.target.value"
              :min="imgAngles.minAngle"
              :max="imgAngles.maxAngle"
          >
        </label>
        </div>

        <button @click="isCatVisible = !isCatVisible">
          {{ isCatVisible ? "Hidden" : "Show" }}
        </button>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PhotoRedactor",
  data() {
    return {
      isCatVisible: true,
      imgFilters: {
        sepia: false,
        border: false,
        shadow: false
      },
      imgSizes: {
        maxWidth: 325,
        maxHeight: 244,
        currentWidth: 325,
        currentHeight: 244
      },
      imgAngles: {
        maxAngle: 360,
        currentAngle: 0
      }
    }
  },
  computed: {
    imgStyles() {
      return{
        width: `${this.imgSizes.currentWidth}px`,
        height: `${this.imgSizes.currentHeight}px`,
        transform: `rotate(${this.imgAngles.currentAngle}deg)`
      }
    }
  }
};
</script>

<style scoped>
.container{
  width: max-content;
  margin: 0 auto;
  font-family: sans-serif;
  font-size: 10px;
}
.flex{
  display: flex;
}
.img-wrapper{
  width: 325px;
  height: 244px;
  margin-right: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #ccc;
}
img{
  transition: .2s ease;
}
img.sepia{
  filter: sepia(100%);
}
img.border{
  border: 3px solid #464646;
}
img.shadow{
  box-shadow: 5px 5px 10px grey;
}
h1{
  font-size: 20px;
  margin: 0 0 10px;
}
h2{
  font-size: 14px;
  margin: 0 0 2px;
}
.btn-group {
  margin-bottom: 15px;
}
button{
  margin-right: 5px;
  background-color: #fff;
  font-size: 10px;
  transition: .2s easy;
}
button.active{
  background-color: grey;
  color: white;
}
label{
  display: flex;
  flex-direction: column;
  margin-right: 10px;
}

</style>