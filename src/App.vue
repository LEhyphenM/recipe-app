<template>
  <div id="app">
    <h1> {{ title }} </h1>
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
    <div v-for="(r, index) of recipes" :key="r.id">
      <fieldset>
        <h1>{{ r.name }}</h1>
        <h2> {{ ingredientsLabel }} </h2>
        <div class="content">{{ r.ingredients }}</div>
        <h2> {{ stepsLabel }} </h2>
        <div class="content">{{ r.steps }}</div>
        <button class="removeBtn" type="button" @click="deleteRecipe(index)">{{ deleteBtn }}</button>
      </fieldset>
    </div>
    <h6> {{ footer }} </h6>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "App",
  data() {
    return {
      title:"Simple Recipe App",
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
      footer: "Lauren Elliott-Manheim • 2015-2022 • Ex astris, scientia"
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
  @mixin styleRemoval {
    box-shadow: none;
    outline: none;
    background-color:transparent;
  }
  @mixin defaultText {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color:$text;
  }
  $size1: 8px;
  $size2: 12px;
  $size3: 18px;
  $size4: 24px;
  $size5: 36px;
  $size6: 48px;
  $background:#224459;
  $text:#F2F2F0;
  $primary:#8599A6;
  $accent:#D5D973;
  $highlight:#B4D930;
  
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
      padding: 20px;
      h1, h2, h6 {color:$highlight;}
      h1 {
        font-weight: bold;
        font-size: 28px;
        text-align: center;
        margin-bottom:30px;
      }
      h2{
        font-size:22px;
        margin:30px auto 10px;
        border-bottom:1px solid $primary;
        display:inline-block;
        }
      h6 {
        font-weight:400;
        letter-spacing:2.25px;
        text-transform:uppercase;
        padding:16px;
        text-align:center;
      }
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
      fieldset{
        border-radius:$size1;
        border-color:$primary;
        padding:20px 30px;
        margin:40px auto;
      }
      .content {
        white-space: pre-wrap;
        margin-top:3px;
      }
      .removeBtn{
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
</style>