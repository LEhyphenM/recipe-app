<template>
  <div id="app">
    <Header />
    <form @submit.prevent="addRecipe">
      <div>
        <label>{{ recipeTitle }}</label>
        <input v-model="recipe.name" />
      </div>
      <div>
        <label>{{ ingredientsLabel }}</label>
        <textarea v-model="recipe.ingredients"></textarea>
      </div>
      <div>
        <label>{{ stepsLabel }}</label>
        <textarea v-model="recipe.steps"></textarea>
      </div>
      <button type="submit">{{ submitBtn }}</button>
    </form>
    <div v-for="(r, index) of recipes" :key="r.id" class="recipe">
      <div class="recipe-content">
        <fieldset>
          <h1>{{ r.name }}</h1>
          <h2> {{ ingredientsLabel }} </h2>
          <div class="content">{{ r.ingredients }}</div>
          <h2> {{ stepsLabel }} </h2>
          <div class="content">{{ r.steps }}</div>
          <button class="removeBtn" type="button" @click="deleteRecipe(index)">{{ deleteBtn }}</button>
        </fieldset>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from './components/Footer.vue';
import { v4 as uuidv4 } from "uuid";
export default {
  name: "App",
  components: {
    Header,
    Footer
  },
  data() {
    return {
      recipeTitle: "Recipe Name",
      ingredientsLabel: "Ingredients",
      stepsLabel: "Steps",
      submitBtn: "Add Recipe",
      deleteBtn: "delete",
      recipe: {
        name: "",
        ingredients: "",
        steps: "",
      },
      recipes: [],
    };
  },
  computed: {
    formValid() {
      const { name, ingredients, steps } = this.recipe;
      return name && ingredients && steps;
    },
  },
  methods: {
    addRecipe() {
      if (!this.formValid) {
        return;
      }
      this.recipes.push({
        id: uuidv4(),
        ...this.recipe,
      });
    },
    deleteRecipe(index) {
      this.recipes.splice(index, 1);
    },
  },
};
</script>

<style lang="scss">
  @import "./scss/variables.scss";
  @import "./scss/mixins.scss";
  body {
    margin: 0;
    padding: 0;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-color: $background;
    color: $text;
    #app {
      max-width: 600px;
      margin:10px auto;
      padding: 20px 20px 0;

      h1, h2, h6 {
        color:$highlight;
      }
      h1 {
        font-size: 28px;
        text-align: center;
      }
      h2 {
        font-size:22px;
        margin:20px auto 3px;
        border-bottom:1px solid $primary;
        display:inline-block;
        }
      // h6 {
      //   font-weight:400;
      //   letter-spacing:2.25px;
      //   text-transform:uppercase;
      //   padding:16px;
      //   text-align:center;
      // }
      form {
        display: flex;
        flex-direction: column;
        width: 100%;
        div {
          margin:7px auto;
          display:grid;
          label {
            font-size: 14px;
            font-weight: bold;
            display:flex;
            text-indent:6px;
            line-height:15px;
          }
        }
        input,
        textarea,
        button {
          @include styleRemoval();
          font-size: 18px;
          padding-left: $size2;
          padding-right: $size2;
          border-radius: $size1;
          margin-top: $size1;
          margin-bottom: $size2;
          min-width:300px;
        }
        input {
          height: $size5;
          background-color: transparent;
          border:1px solid $primary;
          color: inherit;
          &:focus {
            background-color:$primary;
            transition: all 0.65s ease;
          }
        }
        textarea {
          @include defaultText();
          border-radius:$size1;
          border-color:$primary;
          background:transparent;
          line-height:36px;
          &:focus {
            background-color:$primary;
            transition: all 0.65s ease;
          }
        }
        button {
          height:$size6;
          color:$text;
          background-color: $primary;
          border:1px solid $primary;
          font-weight: bold;
          outline: none;
          border-radius: $size1;
          margin-top:30px;
          margin-left:auto;
          margin-right:auto;
          max-width:100%;
          min-width:300px;
          &:hover {
            cursor:pointer;
            background-color: lighten($primary, 10%);
            transition: all 0.65s ease;
          }
        }
      }
      .recipe {
        display: flex;
        flex-direction: column;
        max-width: 500px;
        margin: 0 auto;

        .recipe-content {
          padding: 20px 0 0;
          display: flex;
          margin: 0 auto;
          width: 100%;

          fieldset {
            border-radius:$size1;
            border-color:$primary;
            padding:20px 30px;
            margin:20px auto 10px;
            width:100%;
            h1 {
              margin-bottom:0;
            }
            .content {
              white-space: pre-wrap;
              margin-top:3px;
            }
            .removeBtn {
              height:$size5;
              font-size:18px;
              background-color:transparent;
              outline:none;
              border-radius:$size1;
              color:$text;
              outline:none;
              box-shadow:none;
              border:1px solid $primary;
              padding-left: $size2;
              padding-right: $size2;
              margin:60px auto 10px;
              &:hover {
                cursor:pointer;
                border-color:$primary;
                background-color:$primary;
                transition: all 0.65s ease;
              }
            }
          }
        }
      }
    }
  }

  // X-Small devices (portrait phones, less than 576px)
  @media (max-width: 575.98px) {
    body #app {
      max-width:333px;
      padding:20px 0 10px;
      margin:0 auto;
      form > button {
        margin-top:24px;
      }
      .recipe {
        .recipe-content {
          padding:15px 0 ;
          fieldset{

            h1 {
              margin-bottom:0px;
            }
            h2 {
              margin:20px auto 0;
            }
            .content {
              margin:10px auto 0;
            }
            .removeBtn {
              width:100%;
              margin:30px auto 10px;
            }
          }
        }
      } 
    }
  }
</style>