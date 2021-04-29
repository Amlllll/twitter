<template>
  <div id="app" class="flex container h-screen w-full">
    <div
      class="lg:w-1/5 border-r border-lighter px-2 lg:px-8 py-2 flex flex-col justify-between"
    >
      <div>
        <button
          class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue"
        >
          <i class="fab fa-twitter"></i>
        </button>

        <button
          class=" hover:text-blue flex item-center py-2 px-4 hover:bg-lightblue mr-auto rounded-full mb-3 `${id === tab.id ? 'text-blue' : ''}`"
          @click="id = tab.id"
          v-for="tab in tabs"
          :key="tab.id"
        >
          <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
          <p class="text-lg font-semibold text-left hidden lg:block">
            {{ tab.title }}
          </p>
        </button>

        <button
          class="text-white bg-blue rounded-full font-semibold lg:w-full lg:h-auto h-12 w-12 p-3 hover:bg-darkblue"
        >
          <p class="lg:block hidden">Tweet</p>
          <i class="fas fa-plus lg:hidden"></i>
        </button>
      </div>

      <div class="lg:w-full relative">
        <button
          class="flex items-center w-full rounded-full hover:bg-lightblue p-2"
          @click="dropdown = true"
        >
          <img
            src="./assets/amal.jpg"
            class="h-10 w-10 rounded-full border border-lighter"
          />
          <div class="ml-4 hidden lg:block">
            <p class="text-sm font-bold leading-tight">Amal Elsaeed</p>
            <p class="text-sm leading-tight">@amalelsaeed</p>
          </div>
          <i class="fas fa-angle-down ml-auto text-lg hidden lg:block"></i>
        </button>
        <div
          class="absolute bg-white shadow-md top-div left-0 rounded-lg w-64 border-lightest mr-16"
          v-if="dropdown == true"
        >
          <button
            class="flex items-center w-full rounded-full hover:bg-lightest p-3"
            @click="dropdown = false"
          >
            <img
              src="./assets/amal.jpg"
              class="h-10 w-10 rounded-full border border-lighter"
            />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight">Amal Elsaeed</p>
              <p class="text-sm leading-tight">@amal281294</p>
            </div>
            <i class="fas fa-check ml-auto text-blue"></i>
          </button>

          <button
            @click="dropdown = false"
            class="w-full text-left hover:bg-lightest border-t border-lighter text-sm p-3"
          >
            Add an existing account
          </button>
          <button
            @click="dropdown = false"
            class="w-full text-left hover:bg-lightest border-t border-lighter text-sm p-3"
          >
            Log out @amalelsaeed
          </button>
        </div>
      </div>
    </div>

    <!--tweet!-->
    <div class="h-full w-1/2 sm:w-full overflow-y-scroll">
      <div class="px-5 py-3 border-b border-lighter flex items-center justify-between">
        <h1 class="text-xl font-bold">Home</h1>
        <i class="far fa-star text-xl text-blue"></i>

      </div>
      <div class="px-5 py-3 border-b-8 border-lighter flex">
        <div>
          <img src="./assets/amal.jpg" class="flex-none h-12 w-12 rounded-full border border-lighter">
        </div>
        <form class="w-full px-6 relative" @submit.prevent="addNewTweet">
          <textarea placeholder="whta's up?" class="mt-3 pt-3 w-full focus:outline-none" v-model="tweet.content"></textarea>
          <div class="flex items-center" >
           <i class="text-lg text-blue mr-4 far fa-image"></i>
            <i class="text-lg text-blue mr-4 fas fa-film"></i>
            <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue mr-4 far fa-smile"></i>
          </div>
          <button type="submit" class="h-10 px-4 text-white font-semibold bg-blue hover:bg-darkblue rounded-full absolute right-0 bottom-0">Tweet</button>
        </form>
      </div>
      <div class="flex flex-col-reverse">
        <div  v-for="tweet in tweets" :key="tweet.content" class="w-full p-4 border-b hover:bg-lighter flex">
          <div class="flex-none mr-4">
            <img src="./assets/amal.jpg" class="h-12 w-12 rounded-full flex-none"/>
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold"> Amal Elsaeed</p>
              <p class="text-sm text-dark ml-2"> @amalelsaeed </p>
              <p class="text-sm text-dark ml-2"> 1 sec </p>
              <i class="fas fa-angle-down text-dark ml-auto"></i>
            </div>
            <p class="py-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-comment mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-retweet mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-heart mr-3"></i>
                <p> 1 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-share-square mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="w-full p-4 border-b flex hover:bg-lighter" v-for="follow in following" :key="follow.handle">
        <div class="flex-none mr-4">
          <img src="./assets/p3.jpg" class="rounded-full flex-none h-12 w-12">
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-semibold">{{follow.name}}</p>
            <p class="text-sm text-dark ml-2">{{follow.handle}}</p>
            <p class="text-sm text-dark ml-2">{{follow.time}}</p>
            <i class="fas fa-angle text-dark ml-auto"></i>
          </div>
          <p class="py-2">{{follow.tweet}}</p>
          <div class="flex items-center justify-between w-full">
            <div class="flex items-center text-sm text-dark">
              <i class="mr-3 far fa-comment"></i>
              <p>{{follow.comments}}</p>


            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="mr-3 fas fa-retweet"></i>
              <p>{{follow.retweets}}</p>


            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="mr-3 fas fa-heart"></i>
              <p>{{follow.like}}</p>


            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="mr-3 far fa-share-square"></i>



            </div>


          </div>
        </div>

      </div>

    </div>

    <!--trading!-->
    <div
      class="w-1/3 border-l h-full border-lighter py-2 px-6 overflow-y-scroll relative md:block hidden"
    >
      <input
        class=" pl-12 text-sm rounded-full py-2 w-full bg-lighter"
        placeholder="search twitter"
      />
      <i
        class="fas fa-search absolute top-0 left-0 mt-5 ml-12 text-sm text-light"
      ></i>
      <div class="w-full rounded-lg p-3 bg-lightest">
        <div class="flex items-center justify-between">
          <p class="text-lg font-bold">Trends for you</p>
          <i class="fas fa-cog text-lg text-blue"></i>
        </div>

        <button
          class="w-full flex justify-between hover:bg-lighter p-3 border-t border-lighter"
          v-for="trend in trending"
          :key="trend.title"
        >
          <div>
            <p class="text-sm text-left leading-tight text-dark">
              {{ trend.top }}
            </p>
            <p class="font-bold text-left leading-tight">{{ trend.title }}</p>
            <p class=" text-left leading-tight text-dark">{{ trend.bottom }}</p>
          </div>
          <i class="fas fa-angle-down text-dark text-lg"></i>
        </button>
        <button
          class="p-3 hover:bg-lighter text-left text-blue w-full border-t border-lighter"
        >
          Show more
        </button>
      </div>


        <div class="w-full rounded-lg p-3 bg-lightest my-4">
            <div class="p-3 ">
                <p class="text-lg font-bold">Who to follow</p>

            </div>

            <button
                    class="w-full flex  hover:bg-lighter p-3 border-t border-lighter"
                  v-for="friend in friends " :key="friend.name"
            >
                <img
                        src="./assets/p2.jpg"
                        class="h-12 w-12 rounded-full border border-lighter"
                />
                <div class="ml-4 hidden lg:block">
                    <p class="text-sm font-bold leading-tight">{{friend.name}}</p>
                    <p class="text-sm leading-tight">{{friend.handle}}</p>
                </div>
               <button class=" ml-auto  text-sm text-blue rounded-full py-1 px-4 border-blue border-2">
follow
               </button>


            </button>
            <button
                    class="p-3 hover:bg-lighter text-left text-blue w-full border-t border-lighter"
            >
                Show more
            </button>

        </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tabs: [
        { icon: "fa fa-home", title: "Home", id: "home" },
        { icon: "fa fa-hashtag", title: "Explore", id: "explore" },
        { icon: "fa fa-bell", title: "Notifications", id: "notifications" },
        { icon: "fa fa-envelope", title: "Messages", id: "messages" },
        { icon: "fa fa-bookmark", title: "Bookmarks", id: "bookmarks" },
        { icon: "fas fa-clipboard-list", title: "Lists", id: "lists" },
        { icon: "fa fa-user", title: "Profile", id: "profile" },
        { icon: "fa fa-ellipsis-h", title: "More", id: "more" }
      ],
      id: "home",
      dropdown: false,
      trending: [
        {
          top: "Trending in TX",
          title: "Gigi",
          bottom: "Trending with: Rip Gigi"
        },
        { top: "Music", title: "We Won", bottom: "135K Tweets" },
        { top: "Pop", title: "Blue Ivy", bottom: "40k tweets" },
        { top: "Trending in US", title: "Denim Day", bottom: "40k tweets" },
        { top: "Trending", title: "When Beyonce", bottom: "25.4k tweets" }
      ],
        friends: [
            {src: "./assets/amal.jpg", name: 'Elon Musk', handle: '@teslaBoy'},
            {src: './assets/p2.jpg', name: 'Adrian Monk', handle: '@detective:)'},
            {src: './assets/p3.jpg', name: 'Kevin Hart', handle: '@miniRock'}
        ],
      following: [
        {src: 'elon.jpg', name: 'Elon Musk', handle: '@teslaBoy2', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '1,000', retweets: '550', like: '1,000,003'},
        {src: 'kevin.jpg', name: 'Kevin Hart', handle: '@miniRock', time: '55 min', tweet: 'Should me and the rock do another sub-par movie together????', comments: '2,030', retweets: '50', like: '20,003'},
        {src: 'elon.jpg', name: 'Elon Musk', handle: '@teslaBoy3', time: '1.4 hr', tweet: 'Haha just made a flame thrower. Shld I sell them?', comments: '100,000', retweets: '1,000,002', like: '5,000,003'},
        {src: 'elon.jpg', name: 'Elon Musk', handle: '@teslaBoy4', time: '1.4 hr', tweet: 'Just did something crazyyyyyyy', comments: '100,500', retweets: '1,000,032', like: '5,000,103'}
      ],
      tweets: [
        {content: 'It is so nice outside!'}
      ],
      tweet: {content: ''}

    };
  },
   methods:{
    addNewTweet(){
      let NewTweet = {
        content : this.tweet.content
      }
      this.tweets.push(NewTweet)
    }
   }
};
</script>

<style lang="scss">
button:focus,
input:focus {
  outline: none !important;
}
.top-div {
  top: -9.5rem;
}
</style>
