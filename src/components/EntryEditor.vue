<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import type Emoji from "@/types/Emoji";
import {Ref, ref} from "vue";

const text = ref("");
const emoji: Ref<Emoji | null>= ref(null);
emoji.value = 'fooo';

</script>
<template>
  <form class="entry-form" @submit.prevent>
    <textarea v-model="ref" placeholder="New Journal Entry for danielkelly_io"></textarea>
    <EmojiField />
    <div class="entry-form-footer">
      <span>0 / 280</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
