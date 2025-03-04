<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import type Emoji from "@/types/Emoji";
import {ref, computed, onMounted, inject} from "vue";
import type Entry from "@/types/Entry";
import {userInjectionKey} from "@/types/injectionKeys";

// data
const body = ref("");
const emoji = ref<Emoji | null>(null);
const charCount = computed<number>(() => body.value.length);
const maxChars = 280;
const injectedUser = inject(userInjectionKey)
// events
const emit = defineEmits<{
  (e: "@create", entry: Entry): void
}>();

// template refs
const textarea = ref<HTMLTextAreaElement | null>(null);

onMounted(() => {
  textarea.value?.focus()
})

// methods
const handleTextInput = (e: Event) => {
  const textarea = e.target as HTMLTextAreaElement;
  if (textarea.value <= maxChars) {
    body.value = textarea.value;
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars)
  }
};

const resetData = () => {
  emoji.value = null;
  body.value = "";
}

const onSubmit = () => {
  emit('@create', {
    body: body.value,
    emoji: emoji.value,
    createdAt: new Date(),
    userId: 1,
    id: Math.random()
  })
  resetData();
}

</script>
<template>
  <form
      class="entry-form"
      @submit.prevent="onSubmit"
  >
    <textarea
        ref="textarea" :value="body" @keyup="handleTextInput"
        :placeholder="`New Journal Entry for ${injectedUser?.userName}`"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ charCount }}/ {{ maxChars }}</span>
      <button>Remember
        <ArrowCircleRight width="20" />
      </button>
    </div>
  </form>
</template>
