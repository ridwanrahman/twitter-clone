<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong> {{followers}}
            </div>
            <form class="user-profile__create-tweet" @submit.prevent="createNewTweet" :class="{'--exceeded': newTweetCharacterCount > 180 }">
                <label for="newTweet"><strong>New Tweet</strong>({{newTweetCharacterCount}}/180)</label>
                <textarea id="newTweet" rows="4" v-model="newTweetContent">
                </textarea>

                <div class="user-profile__create-tweet-type">
                    <label for="newTweetType"><strong>Type: </strong></label>
                    <select id="newTweetType" v-model="selectedTweetType">
                        <option :value="option.value" v-for="(option,index) in tweetTypes" :key="index">
                            {{ option.name }}
                        </option>
                    </select>
                </div>
                <button>
                    Tweet!
                </button>
            </form>
        </div>
        <div class="user-profile__tweets-wrapper">
            <TweetItem v-for="tweet in user.tweets" 
                        :key="tweet.id" 
                        :username="user.username" 
                        :tweet="tweet"
                        @favourite="toggleFavourite"/>
        </div>
    </div>    
</template>

<script>
import TweetItem from "./Tweetitem";

export default {
    name: 'UserProfile',
    components: { TweetItem },
    data() {
        return {
            newTweetContent: '',
            selectedTweetType: 'instant',
            tweetTypes: [
                {value: 'draft', name: 'Draft'},
                {value: 'instant', name: 'Instant Tweet'}
            ],
            followers: 0,
            user: {
                id: 1,
                username: '_Ridwanur Rahman',
                firstName: "Ridwan",
                lastName: "Rahman",
                email: 'ridwanrahman07@gmail.com',
                isAdmin: true,
                tweets: [
                    {id:1, content: 'Twitter is amazing'},
                    {id:2, content: 'Dont forget to subscribe'}
                ]
            }
        }
    },
    watch: {
        followers(newFollowerCount, oldFollowerCount) {
            if(oldFollowerCount < newFollowerCount) {
                console.log(`${this.user.username} has gained a follower`);
            }
        }
    },
    computed: {
        fullName() {
            // console.log("full name function");
            return `${this.user.firstName} ${this.user.lastName}`;
        },
        newTweetCharacterCount() {
            return this.newTweetContent.length;
        }
    },
    methods: {
        followUser() {
            // console.log("follow user button clicked");
            this.followers++;
        },
        toggleFavourite(id) {
            console.log("here");
            console.log(`Favourite tweet #${id}`);
        },
        createNewTweet() {
            if(this.newTweetContent && this.selectedTweetType != 'draft') {
                this.user.tweets.unshift( {
                    id:this.user.tweets.length + 1,
                    content: this.newTweetContent
                })
                this.newTweetContent = '';
            }
        }
    },
    beforeCreate() {
        // console.log("before create function");
    },
    created() {
        // console.log("created function");
    },
    beforeMount() {
        // console.log("before mount");
    },
    beforeUpdate() {
        // console.log("before update");
    },
    updated() {
        // console.log("updated");
    },
    mounted() {
        // console.log("mounted");
        this.followUser();
    }
}
    
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
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #DFE3E8;
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

        .user-profile__create-tweet {
            padding-top: 20px;
            display: flex;
            flex-direction: column;

            &.--exceeded {
                color:red;
                border-color: red;
                button {
                    background-color: red;
                    border:none;
                    color:white;
                }
            }
        }
        .user-profile__tweets-wrapper{
            display: grid;
            grid-gap: 10px;
            margin-bottom: auto;
        }
    }
}



</style>