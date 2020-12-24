<template>
    <!-- <div class="user-profile">
        {{ user.username }}
    </div> -->
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong> {{followers}}
            </div>
        </div>

        <div class="user-profile__tweets-wrapper">
            <TweetItem v-for="tweet in user.tweets" 
                        :key="tweet.id" 
                        :username="user.username" 
                        :tweet="tweet"/>
        </div>


        <div class="user-profile__tweets-wrapper">
            <div class="user-profile__tweet" v-for="tweet in user.tweets" :key="tweet.id">
                asdfasf
            </div>
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
        }
    },
    methods: {
        followUser() {
            // console.log("follow user button clicked");
            this.followers++;
        },
        toggleFavourite(id) {
            console.log(`Favourite tweet #${id}`);
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

<style>
.user-profile {
    display: grid;
    /* background-color: white; */
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}
.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}
.user-profile__admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px; 
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;

}
h1 {
    margin: 0;
}
</style>