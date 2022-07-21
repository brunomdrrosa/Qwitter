<template>
  <q-page class="relative-position">
    <q-scroll-area class="absolute full-width full-height">
      <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
          <q-input
            bottom-slots
            v-model="newQweetContent"
            class="new-qweet"
            placeholder="O que está acontecendo?"
            counter
            maxlength="280"
            autogrow
          >
            <template v-slot:before>
              <q-avatar size="xl">
                <img src="https://i.imgur.com/HYOe5LV.jpg" />
              </q-avatar>
            </template>
          </q-input>
        </div>
        <div class="col col-shrink">
          <q-btn
            @click="addNewQweet"
            :disable="!newQweetContent"
            class="q-mb-lg"
            color="primary"
            label="Qweet"
            rounded
            unelevated
            no-caps
          />
        </div>
      </div>
      <q-separator class="divider" size="10px" color="grey-2" />
      <q-list separator>
        <transition-group
          appear
          enter-active-class="animated fadeIn slow"
          leave-active-class="animated fadeOut slow"
        >
          <q-item v-for="qweet in qweets" :key="qweet.id" class="qweet q-py-md">
            <q-item-section avatar top>
              <q-avatar size="xl">
                <img src="https://i.imgur.com/HYOe5LV.jpg" />
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label class="text-subtitle1"
                ><strong>Usuário do Qwitter</strong>
                <span class="text-grey-7">
                  @brunomdrrosa <br class="lt-md" />&bull;
                  {{ relativeDate(qweet.date) }}</span
                ></q-item-label
              >
              <q-item-label class="qweet-content text-body1">
                {{ qweet.content }}
              </q-item-label>
              <div class="qweet-icons row justify-between q-mt-sm">
                <q-btn
                  color="grey"
                  icon="far fa-comment"
                  size="sm"
                  flat
                  round
                ></q-btn>
                <q-btn
                  color="grey"
                  icon="fas fa-retweet"
                  size="sm"
                  flat
                  round
                ></q-btn>
                <q-btn
                  @click="toggleLiked(qweet)"
                  :color="qweet.liked ? 'pink' : 'grey'"
                  :icon="qweet.liked ? 'fas fa-heart' : 'far fa-heart'"
                  size="sm"
                  flat
                  round
                ></q-btn>
                <q-btn
                  @click="deleteQweet(qweet)"
                  color="grey"
                  icon="fas fa-trash"
                  size="sm"
                  flat
                  round
                ></q-btn>
              </div>
            </q-item-section>
          </q-item>
        </transition-group>
      </q-list>
    </q-scroll-area>
  </q-page>
</template>

<script>
import db from "src/boot/firebase";
import {
  collection,
  getDocs,
  orderBy,
  query,
  addDoc,
  onSnapshot,
  deleteDoc,
  doc,
  updateDoc,
} from "firebase/firestore";
import { defineComponent } from "vue";
import { formatDistance } from "date-fns";

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newQweetContent: "",
      qweets: [],
    };
  },
  methods: {
    relativeDate(value) {
      return formatDistance(value, new Date());
    },
    async addNewQweet() {
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now(),
        liked: false,
      };
      const docRef = await addDoc(collection(db, "qweets"), newQweet);
      this.newQweetContent = "";
    },
    async deleteQweet(qweet) {
      let IDsCantBeRemoved = [
        "QPmEdZqkkszpEB7Z11Fk",
        "y76Sz5s63NGsHYEEBveA",
        "72wKtb4AHbcF8roFiL84",
      ];
      if (IDsCantBeRemoved.includes(qweet.id)) {
        console.log("Este tweet não pode removido");
      } else {
        await deleteDoc(doc(db, "qweets", qweet.id));
      }
    },
    async toggleLiked(qweet) {
      await updateDoc(doc(db, "qweets", qweet.id), {
        liked: !qweet.liked,
      });
    },
  },
  async mounted() {
    const ordersRef = collection(db, "qweets");
    const q = query(ordersRef, orderBy("date"));

    const unsubscribe = onSnapshot(q, (snapshot) => {
      snapshot.docChanges().forEach((change) => {
        let qweetChange = change.doc.data();
        qweetChange.id = change.doc.id;
        if (change.type === "added") {
          this.qweets.unshift(qweetChange);
        }
        if (change.type === "modified") {
          let index = this.qweets.findIndex(
            (qweet) => qweet.id === qweetChange.id
          );
          Object.assign(this.qweets[index], qweetChange);
        }
        if (change.type === "removed") {
          let index = this.qweets.findIndex(
            (qweet) => qweet.id === qweetChange.id
          );
          this.qweets.splice(index, 1);
        }
      });
    });
  },
});
</script>

<style lang="sass">
.new-qweet
  textarea
    font-size: 19px
    line-height: 1.4 !important
.divider
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4
.qweet-content
  white-space: pre-line
.qweet-icons
  margin-left: -5px
</style>
