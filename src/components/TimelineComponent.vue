<template lang="html">
  <div class="container mt-5 mb-5">
    <b-row>
      <b-col lg="12">
        <h4 class="text-center">
          Latest News
        </h4>
        <ul class="timeline">
          <li 
            v-for="item in items"
            :key="item.id"
          >
            <div id="user-info">
              <img
                class="user-pic"
                src="https://cdn2.iconfinder.com/data/icons/ios-7-icons/50/user_male2-512.png"
                alt="user-img"
              >
              <span class="p-3">
                <strong>User name</strong>
              </span>
              <span class="float-right py-3">
                <b>
                  3 Hours ago
                </b>
              </span>
            </div>
            <div
              style=" padding-left: 1.7em; padding-bottom: 2em; width: 600px;"
              class="fw-semi-bold p-4 pl-5"
            >
              <b-row>
                <b-col
                  lg="1.5"
                  xs="12"
                >
                  <div>
                    <img
                      class="emoji"
                      width="70px"
                      src="/img/netural.006cc26d.png"
                      alt=""
                    >
                    <h3 class="text-center">
                      <strong>14%</strong>
                    </h3>
                  </div>
                </b-col>
                <b-col
                  lg="1.5"
                  xs="12"
                >
                  <div>
                    <div>
                      <img
                        class="emoji"
                        width="70px"
                        src="/img/netural.006cc26d.png"
                        alt=""
                      >
                      <h3 class="text-center">
                        <strong>13%</strong>
                      </h3>
                    </div>
                  </div>
                </b-col>
                <b-col
                  lg="1.5"
                  xs="12"
                >
                  <div>
                    <div>
                      <img
                        class="emoji"
                        width="70px"
                        src="/img/netural.006cc26d.png"
                        alt=""
                      >
                      <h3 class="text-center">
                        <strong>33%</strong>
                      </h3>
                    </div>
                  </div>
                </b-col>
                <b-col
                  lg="1.5"
                  xs="12"
                >
                  <div>
                    <div>
                      <img
                        class="emoji"
                        width="70px"
                        src="/img/netural.006cc26d.png"
                        alt=""
                      >
                      <h3 class="text-center">
                        <strong>7%</strong>
                      </h3>
                    </div>
                  </div>
                </b-col>
                <b-col
                  lg="1.5"
                  xs="12"
                >
                  <div>
                    <div>
                      <img
                        class="emoji"
                        width="70px"
                        src="/img/netural.006cc26d.png"
                        alt=""
                      >
                      <h3 class="text-center">
                        <strong>28%</strong>
                      </h3>
                    </div>
                  </div>
                </b-col>
                <b-col
                  lg="1.5"
                  xs="1"
                >
                  <div>
                    <div>
                      <img
                        class="emoji"
                        width="70px"
                        src="/img/netural.006cc26d.png"
                        alt=""
                      >
                      <h3 class="text-center">
                        <strong>3%</strong>
                      </h3>
                    </div>
                  </div>
                </b-col>
                <b-col
                  lg="1.5"
                  xs="12"
                >
                  <div>
                    <div>
                      <img
                        class="emoji"
                        width="70px"
                        src="/img/netural.006cc26d.png"
                        alt=""
                      >
                      <h3 class="text-center">
                        <strong>2%</strong>
                      </h3>
                    </div>
                  </div>
                </b-col>
              </b-row>
            </div>
          </li>
        </ul>
      </b-col>
    </b-row>
  </div>
</template>

<script lang="js">
  import { EMOTIONS } from '../graphql/Mutations';

  
  export default {
    name: 'TimelineComponent',
    data () {
      return {
        items: []
      }
    },
    mounted() {
      // console.log(this.items)
    },
    // apollo: {
    //   items: {
    //     query: EMOTIONS
    //   }
    // }
    // apollo: {
    //   subscribeToMore: [
    //   {
    //     document: FETCH_REAL_EMOTIONS,
    //     updateQuery: (previous, { subscriptionData }) => {
    //       console.log('updateQuery', previous, subscriptionData)
    //       // const newAllLinks = [
    //       //   subscriptionData.data.Link.node,
    //       //   ...previous.allLinks
    //       // ]
    //       // const result = {
    //       //   ...previous,
    //       //   allLinks: newAllLinks.slice(0, 5)
    //       // }
    //       // return result
    //     }
    //   }
    // ]
    // }
  }
</script>

<style scoped lang="scss">
ul.timeline {
  list-style-type: none;
  position: relative;
  width: 620px;
}
ul.timeline:before {
  content: ' ';
  background: red;
  display: inline-block;
  position: absolute;
  left: 29px;
  width: 2px;
  height: 100%;
  z-index: -2;
}
ul.timeline > li {
  margin: 41px 0;
  padding-left: 52px;
}
// ul.timeline > li:before {
//     content: ' ';
//     background: white;
//     display: inline-block;
//     position: absolute;
//     border-radius: 50%;
//     border: 3px solid #22c0e8;
//     left: 20px;
//     width: 20px;
//     height: 20px;
//     z-index: 400;
// }
.emoji {
  margin-right: 11px;
}
.user-pic {
  border-radius: 50%;
  width: 50px;
  height: 50px;
  margin-left: -46.8px;
  z-index: -1;
}
</style>