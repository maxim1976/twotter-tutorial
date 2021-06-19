<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{ user.username }}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
              Admin
            </div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong> {{ followers }}
            </div>
            <form class="user-profile__creat-twoot">
              <label for="newTwoot"><strong>New Twoot</strong></label>
              <textarea id="newTwoot" rows="4"/>
              <div class="user-profile__create-twoot-type">
                <label for="newTwootType"><strong>Type: </strong></label>
                <select id="newTwootType">
                  
                  <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
                    {{ option.name }}
                </select>

              </div>
            </form>
        </div>
        <div class="user-profile__twoots-wrapper">
          <TwootItem 
              v-for="twoot in user.twoots" 
              :key="twoot.id" :username="user.username" 
              :twoot="twoot" 
              @favourite="toggleFavourite"/>
        </div>
    </div> 
</template>

<script>
import TwootItem from "./TwootItem.vue";


export default {
    name: "UserProfile",
    components: { TwootItem },
    data() {
      return {
        twootTypes: [
          { value: 'draft', name: 'Draft' },
          { value: 'instant', name: 'Instant Twoot' }

        ],
        followers: 0,
        user:{
          id: 1,
          username: '_MaximDongur-ool',
          firstName: 'Maxim',
          lastName: "Dongur-ool",
          email: 'maximdongurool@gmail.com',
          isAdmin: true,
          twoots: [
            { id: 1, content: 'Twooter is amazing!' },
            { id:2, content: 'Dont forget the Earth is square!' }
          ]
        }
      }
    },
    watch: {
      followers(newFollowerCount, oldFollowerCount) {
        if (oldFollowerCount < newFollowerCount) {
          console.log(`${this.user.username} has gained a follower!`)
        }
      }
    },
    computed: {
      fullName() {
        return `${this.user.firstName} ${this.user.lastName}`;
      }
    },
    methods: {
      followUser() {
        this.followers ++
      },
      toggleFavourite(id) {
        console.log(`Favourited Tweet #${id}`)
      }
    },
    mounted() {
      this.followUser();
    }
}

</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #2c3e50;
    border-radius: 5px;
    border:  1px solid #DFE3E8;
}

.user-profile__admin-badge {
  background: red;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
  
}

h1 {
    margin: 0;
}

.user-profile__twoots-wrapper {
  display: grid;
  grid-gap: 10px;
}

.user-profile__create-twoot {
  padding-top: 20px;
  display: flex;
  flex-direction: column;
}
</style>
