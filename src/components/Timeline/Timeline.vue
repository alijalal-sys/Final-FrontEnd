<template>
  <aside :class="{chat: true, chatOpen}">
    <header class="chatHeader">
      <h4 class="chatTitle text-center">
        Live Feed
      </h4>
      <div class="chatSearch text-center">
        <strong>
          Here's a Live feed for User's emotions
        </strong>
      </div>
    </header>
    <div :class="{'chatPanel chatContacts': true, chatMessageOpen: chatMessageOpened}">
      <h5 class="navTitle">
        TODAY
      </h5>
      <b-list-group
        id="chat-sidebar-user-group"
        class="chatSidebarUserGroup"
      >
        <b-list-group-item
          v-for="emotion in emotions"
          :key="emotion._id"
        >
          <div>
            <span class="thumb-sm float-left">
              <img
                class="rounded-circle"
                src="https://cdn2.iconfinder.com/data/icons/ios-7-icons/50/user_male2-512.png"
                alt="..."
              >
            </span>
          </div>
          <div>
            <h6 class="messageSender">
              {{ emotion.userId }}
            </h6>
            <div
              style=" padding-left: 1.7em; padding-bottom: 2em; width: 100%;"
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
                      width="38px"
                      src="../../assets/img/neutral.svg"
                      alt=""
                    >
                    <h6 class="text-center">
                      <b> {{ emotion.neutral }} </b>
                    </h6>
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
                        width="38px"
                        src="../../assets/img/happy.svg"
                        alt=""
                      >
                      <h6 class="text-center">
                        <b> {{ emotion.happy }} </b>
                      </h6>
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
                        width="38px"
                        src="../../assets/img/sad.svg"
                        alt=""
                      >
                      <h6 class="text-center">
                        <b> {{ emotion.sad }} </b>
                      </h6>
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
                        width="38px"
                        src="../../assets/img/angry.svg"
                        alt=""
                      >
                      <h6 class="text-center">
                        <b> {{ emotion.angry }} </b>
                      </h6>
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
                        width="38px"
                        src="../../assets/img/fearful.svg"
                        alt=""
                      >
                      <h6 class="text-center">
                        <b> {{ emotion.fearful }} </b>
                      </h6>
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
                        width="38px"
                        src="../../assets/img/disgusted.svg"
                        alt=""
                      >
                      <h6 class="text-center">
                        <b>{{ emotion.disgusted }}</b>
                      </h6>
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
                        width="38px"
                        src="../../assets/img/surprised.svg"
                        alt=""
                      >
                      <h6 class="text-center">
                        <b>{{ emotion.surprised }}</b>
                      </h6>
                    </div>
                  </div>
                </b-col>
              </b-row>
            </div>
          </div>
        </b-list-group-item>
      </b-list-group>
    </div>
    <div :class="{'chatPanel chatMessages': true, chatMessageOpen: !chatMessageOpened}">
      <h6 class="messagesTitle">
        <a @click="chatMessageOpened = true">
          <i class="fa fa-angle-left mr-xs" />
          {{ conversation.name }}
        </a>
      </h6>
    </div>
  </aside>
</template>

<script>
import Vue from 'vue';
import { mapState, mapActions } from 'vuex';
import { FACE_DETECTING_SUBSCRIPTIOM, EMOTIONS_QUERY } from '../../graphql/Mutations'
import { MessageStates } from '../../store/layout';

export default {
  name: 'Timeline',
  data() {
    return {
      messageStates: MessageStates,
      chatMessageOpened: true,
      conversation: Object,
      searchValue: '',
      render: false,
    };
  },
  computed: {
    ...mapState('layout', ['chatOpen', 'chatNotificationMessageState']),
  },
  methods: {
    ...mapActions('layout', ['readMessage']),
    filterConversations(item) {},
    handleSearchInput(value) {
      Vue.set(this, 'searchValue', value);
    },
    openMessages(conversation, index) {
      Vue.set(this, 'conversation', conversation);
      Vue.set(this, 'chatMessageOpened', false);

      if (index === 0) {
        this.readMessage();
      }
    },
    addMessage(e) {},
  },
  // watch: {
  //   emotions: {
  //     deep: true,

  //     handler () {
  //       if (this.emotions.length === 0) return;
  //       this.render = true;
  //     }
  //   }
  // },
  apollo: {
    emotions: {
      query: EMOTIONS_QUERY,
      subscribeToMore: {
        document: FACE_DETECTING_SUBSCRIPTIOM,
        updateQuery: function (previousData, { subscriptionData }) {
          previousData.emotions.push({
            _id: "User",
            neutral: 0.9990482330322266,
            happy: 0.00009672110172687098,
            sad: 2.7655198664433556e-7,
            angry: 2.7222253606851154e-7,
            fearful: 1.324585525708244e-7,
            disgusted: 9.08449038217185e-10,
            surprised: 0.0008544266456738114,
            userId: "5e458c4f18efe23924514b58",
            createdAt: "1581969855237"
          })
          return {
            emotions: [
              subscriptionData.data.faceDetected,
              ...previousData.emotions,
            ]
          }
        }
      }
    }
  }
};
</script>

<style src="./Timeline.scss" lang="scss" />
