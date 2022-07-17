<template>
  <q-page>
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
              <img
                src="https://pbs.twimg.com/profile_images/1391831038511521794/izFarcRT_400x400.jpg"
              />
            </q-avatar>
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn
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
    <q-list>
      <q-item class="q-py-md">
        <q-item-section avatar top>
          <q-avatar size="xl">
            <img
              src="https://pbs.twimg.com/profile_images/1391831038511521794/izFarcRT_400x400.jpg"
            />
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1"
            ><strong>Bruno Machado</strong
            ><span class="text-grey-7">@brunomdr02</span></q-item-label
          >
          <q-item-label class="qweet-content text-body1">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque ac
            commodo est. Donec fringilla consectetur leo, et eleifend sem
            hendrerit vel.
          </q-item-label>
          <div class="qweet-icons row justify-between q-mt-sm">
            <q-btn color="grey" icon="far fa-comment" size="sm" flat round></q-btn>
            <q-btn color="grey" icon="fas fa-retweet" size="sm" flat round></q-btn>
            <q-btn color="grey" icon="far fa-heart" size="sm" flat round></q-btn>
            <q-btn color="grey" icon="fas fa-trash" size="sm" flat round></q-btn>
          </div>
        </q-item-section>

        <q-item-section side top> 1 min ago </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newQweetContent: "",
    };
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
