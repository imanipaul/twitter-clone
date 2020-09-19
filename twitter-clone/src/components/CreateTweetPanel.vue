<template>
  <form
    class="create-tweet-panel"
    @submit.prevent="createNewTweet"
    :class="{'--exceeded':newTweetCharacterCount > 180}"
  >
    <label for="newTweet">
      <strong>New Tweet</strong>
      ({{ newTweetCharacterCount}} / 180)
    </label>
    <textarea id="newTweet" rows="4" v-model="newTweetContent" />
    <div class="create-tweet-panel__submit">
      <div class="create-tweet-type">
        <label for="newTweetType">
          <strong>Type:</strong>
        </label>
        <select id="newTweetType" v-model="selectedTweetType">
          <option
            v-for="option in tweetTypes"
            :value="option.value"
            :key="option.value"
          >{{ option.name }}</option>
        </select>
      </div>
      <button>Tweet!</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "CreateTweetPanel",
  data() {
    return {
      newTweetContent: "",
      selectedTweetType: "instant",
      tweetTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Tweet" },
      ],
    };
  },
  computed: {
    newTweetCharacterCount() {
      return this.newTweetContent.length;
    },
  },
  methods: {
    createNewTweet() {
      if (this.newTweetContent && this.selectedTweetType !== "draft") {
        this.$emit("add-tweet", this.newTweetContent);
        this.newTweetContent = "";
      }
    },
  },
};
</script>

<style lang='scss' scoped>
.create-tweet-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;

  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }

  .create-tweet-panel__submit {
    display: flex;
    justify-content: space-between;

    .create-tweet-type {
      padding: 10px 0;
    }

    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: rebeccapurple;
      color: white;
      font-weight: bold;
    }
  }

  &.--exceeded {
    color: red;
    border-color: red;

    .create-tweet-panel__submit {
      button {
        background-color: red;
        border: none;
        color: white;
      }
    }
  }
}
</style>