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
</style>
