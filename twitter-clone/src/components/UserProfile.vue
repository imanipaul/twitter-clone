<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{user.username}}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile__follower-count">
          <strong>Followers:</strong>
          {{followers}}
        </div>
      </div>
      <CreateTweetPanel @add-tweet="addTweet" />
    </div>
    <div class="user-profile__tweets-wrapper">
      <TweetItem
        v-for="tweet in user.tweets"
        :key="tweet.id"
        :username="user.username"
        :tweet="tweet"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem";
import CreateTweetPanel from "./CreateTweetPanel";

export default {
  name: "UserProfile",
  components: { CreateTweetPanel, TweetItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_imanip",
        firstName: "Imani",
        lastName: "Paul",
        email: "imanipaul@email.com",
        isAdmin: true,
        tweets: [
          { id: 1, content: "Twitter is Amazing!!" },
          { id: 2, content: "Don't forget to subscribe" },
        ],
      },
    };
  },
  methods: {
    addTweet(tweet) {
      this.user.tweets.unshift({
        id: this.user.tweets.length + 1,
        content: tweet,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    margin-bottom: auto;

    h1 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }

  .user-profile__tweets-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>
