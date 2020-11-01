<template>
    <div class="user-profile">
        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{user.username}}</h1>
            <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
            <div class="user-profile_admin-badge" v-else>Not Admin</div>
            <div class="user-profile_follower-count">
                <strong>Followers: </strong> {{followers}}
            </div>
        </div>
        <div class="user-profile_twoots-wrapper">
            <TwootItem
                v-for="twoot in user.twoots"
                :key="twoot.id"
                :username="user.username"
                :twoot="twoot"
                @favourite="toggleFavourite"/>
        </div>
    </div>
</template>

<script>
    import TwootItem from "./TwootItem";
    export default {
        name: "UserProfile",
        components: {TwootItem},
        data(){
            return{
                followers: 0,
                user: {
                    id: 1,
                    username: 'beastlee_23',
                    firstname: 'Brandon Lee',
                    lastname: 'Naidoo',
                    email: 'brandon.naidoo@dimensiondata.com',
                    isAdmin: true,
                    twoots: [
                        {id: 1, content: 'Twotter is amazing!'},
                        {id: 2, content: "Don't forget to subscribe to The Earth is Square!"}
                    ]
                }
            }
        },
        watch: {
            followers(newFollowerCount, OldFollowerCount){
                if(OldFollowerCount < newFollowerCount)
                {
                    console.log(`${this.user.username} has gained a follower!`);
                }
            }
        },
        computed: {
            fullname() {
                return `${this.user.firstname} ${this.user.lastname}`;
            }
        },
        methods:{
            followUser() {
                this.followers++;
            },
            toggleFavourite(id){
             console.log(`Favourited Tweet #${id}`);
            }
        },
        mounted() {
            this.followUser();
        }
    }
</script>

<style>
    .user-profile{
        display: grid;
        grid-template-columns: 1fr 3fr;
        width: 100%;
        padding: 50px 5%;
    }

    .user-profile_user-panel{
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #DFE3E8;
    }

    h1{
        margin: 0;
    }

    .user-profile_admin-badge
    {
        background: rebeccapurple;
        color: white;
        border-radius: 5px;
        margin-right: auto;
        padding: 0 10px;
        font-weight: bold;
    }

</style>