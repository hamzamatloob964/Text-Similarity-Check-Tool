<template>
  <div class="main-cont">
    <div class="main-cont-heading">
      <h1>Welcome to Text Similarity Tool</h1>
    </div>

    <div class="main-cont-content">
      <div class="similarity-input-cont row-flex-cont">
        <v-hover v-slot="{ hover }" close-delay="200">
          <v-card class="input-cont-card" :elevation="hover ? 16 : 2">
            <v-select
              :items="items"
              label="Select Language"
              density="compact"
              class="lang-select margin-top-10 width-80"
              v-model="language"
            ></v-select>
            <v-textarea
              name="input-7-1"
              variant="filled"
              clearable
              no-resize
              clear-icon="mdi-close-circle"
              class="margin-top-5 width-80"
              bg-color="grey-lighten-2"
              label="Text #1"
              v-model="text1"
            ></v-textarea>
    
            <v-textarea
              name="input-7-1"
              variant="filled"
              clearable
              no-resize
              clear-icon="mdi-close-circle"
              class="margin-top-5 width-80"
              bg-color="grey-lighten-2"
              label="Text #2"
              v-model="text2"
            ></v-textarea>
    
            <v-btn @click="submit" color="primary" density="default" class="btn-check-similarity margin-bottom-10">Check Similarity</v-btn>
    
          </v-card>
        </v-hover>
          
      </div>

      <div class="similarity-output-cont row-flex-cont">
        <v-hover v-slot="{ hover }" close-delay="200">
          <v-card class="output-cont-card" :elevation="hover ? 16 : 2">
            <div class="flex-cont">
              <v-icon>mdi-home</v-icon>
              <span>Graph recomender</span>
            </div>
            <div class="flex-cont">
              <v-icon>mdi-home</v-icon>
              <span>User profile</span>
            </div>
            <div class="flex-cont">
              <v-icon>mdi-home</v-icon>
              <span>Text Similarity</span>
            </div>
            <v-divider class="margin-bottom-10 margin-top-10 width-80"></v-divider>
            <span class="margin-top-10">Please select the text type</span>
            <v-radio-group v-model="active">
              <v-radio class="margin-top-10" label="Title similarity (short text)" :value="shortText"></v-radio>
              <v-radio class="margin-top-10" label="Description similarity (long text)" :value="longText"></v-radio>
            </v-radio-group>
            <span>Short text similarity threshold-En</span>
            <v-range-slider
              v-model="shortEnRange"
              step="1"
              :max="10"
              :min="-10"
              thumb-label=""
            ></v-range-slider>
            <span>Short text similarity threshold-De</span>
            <v-range-slider
              v-model="shortDeRange"
              step="1"
              :max="10"
              :min="-10"
              thumb-label=""
            ></v-range-slider>
            <span>Long text similarity threshold-En</span>
            <v-range-slider
              v-model="longEnRange"
              step="1"
              :max="10"
              :min="-10"
              thumb-label=""
            ></v-range-slider>
            <span>Long text similarity threshold-De</span>
            <v-range-slider
              v-model="longDeRange"
              step="1"
              :max="10"
              :min="-10"
              thumb-label=""
            ></v-range-slider>
          </v-card>
        </v-hover>
    
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TextSimilarityCheck',
  data() {
    return {
      items: ['English', 'German'],
      text1:"",
      text2:"",
      shortText:"shortText",
      longText:"longText",
      active:"shortText",
      language:"",
      shortEnRange:[-3,5],
      shortDeRange:[-6,9],
      longEnRange:[-2,8],
      longDeRange:[-4,7]
    }
  },
  methods: {
    submit () {
      var obj={}
      obj.text1=this.text1
      obj.text2=this.text2
      obj.textType=this.active
      obj.language=this.language

      const baseURI = 'http://127.0.0.1:8000/items'
      this.$http.post(baseURI,obj)
      .then((result) => {
        console.log("show response......... :",result.data)
      })
    }
  },
    
}
</script>

<style scoped>
.main-cont{
  display: flex;
  flex-direction: column;
  /* overflow-y: hidden; */
}
.main-cont-content{
  display: flex;
  flex-direction: row-reverse;
}
.main-cont-heading{
  width: 100vw;
  height: 80px;
  /* background-color: gray; */
  display: flex;
  justify-content: center;
  align-items: center;
}
.similarity-input-cont{
  /* background-color: red; */
  width: 50vw;
  height: 620px;
}
.similarity-output-cont{
  /* background-color: green; */
  width: 50vw;
  height: 620px;
}
.input-cont-card{
  width: 80%;
  height: 90%;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* background-color: gray; */
}
.output-cont-card{
  width: 80%;
  height: 90%;
  display: flex;
  flex-direction: column;
  padding: 8px;
  /* align-items: center; */
  /* background-color: gray; */
}
.row-flex-cont{
  display: flex;
  justify-content: center;
  align-items: center;
}
.flex-cont{
  display: flex;
}
.lang-select{
}
.margin-left-10{
  margin-left: 10px;
}
.margin-top-10{
  margin-top: 10px;
}
.margin-top-5{
  margin-top: 5px;
}
.margin-bottom-10{
  margin-bottom: 10px;
}
.width-80{
  width: 80%;
}
.height-50px{
  height: 50px;
}
.btn-check-similarity{
  width: 200px;
}
    
</style>