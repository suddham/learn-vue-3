<template>
  <div class="mx-auto max-w-6xl text-center py-6">
    <h1 class="font-bold text-4xl py-10">VMail Inbox</h1>
    <table class="table-auto">
      <thead>
        <tr>
          <th class="px-4 py-2"></th>
          <th class="px-4 py-2">From</th>
          <th class="px-4 py-2">Subject</th>
          <th class="px-4 py-2">Sent At</th>
        </tr>
      </thead>

      <tbody>
        <tr
          v-for="email in unArchivedEmails"
          :key="email.id"
          class="pointer-events-auto cursor-pointer even:bg-gray-100 odd:bg-gray-200"
          :class="[
            email.read
              ? 'text-gray-400 bg-gray-900 line-through'
              : 'text-gray-800',
          ]"
          v-on:click="email.read = !email.read"
        >
          <td class="border px-4 py-2"><input type="checkbox" /></td>
          <td class="border px-4 py-2">{{ email.from }}</td>
          <td class="border px-4 py-2">
            <p>
              <span class="font-semibold">{{ email.subject }}</span>
              -
              <span class="">{{ email.body }}</span>
            </p>
          </td>
          <td class="border px-4 py-2 mx-4">
            {{ format(new Date(email.sentAt), "MMM do yyyy") }}
          </td>
          <td>
            <button
              class="px-4 py-2 bg-gray-800 text-white rounded mx-4"
              @click="email.archived = true"
            >
              Archive
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { format } from "date-fns";

export default {
  name: "App",
  data() {
    return {
      format,
      emails: [
        {
          id: 1,
          from: "team@vuemastery.com",
          subject:
            "What's up with Vue 3.0? Here's how to find out from Evan You",
          body:
            "The opening keynote of VueConf US this year was Evan You (the creator of Vue), giving his State of the Vuenion address. He walked us through the journey of getting Vue 3 from a prototype to a reality the past year. He also dove into Vue's overall growth in the community.",
          sentAt: "2020-03-27T18:25:43.511Z",
          archived: false,
          read: true,
        },
        {
          id: 2,
          from: "jeffrey@vuetraining.net",
          subject: "Learn by doing - Vue 3 Zero to Intermediate in 8 weeks",
          body:
            "Building projects is one of the most effective ways to learn - and _the_ most effective way _remember_ what you've learned - but it can be frustrating.\n\nThis 8-week course takes the pain out of 'learning by doing'.\n\nEach week we give you\n\n* a project that will grow your skills without overwhelming you\n* links to hand-picked resources, such as Vue Mastery videos, that share the knowledge you'll need for the project (no more useless rabbit holes)\n* answers to any and all questions you have while working\n* feedback on your completed code (so you're only learning good habits)\n\nOur instructors are standing by to answer your questions.\n\nReady to learn?",
          sentAt: "2020-05-20T18:25:43.511Z",
          archived: false,
          read: false,
        },
        {
          id: 3,
          from: "damian@dulisz.com",
          subject:
            "#177: Updated Vue.js Roadmap; Vuex v4.0.0-alpha.1 has been released; Kia King Ishii join the core team; Nuxt v2.12 released; Videos from Vue.js Amsterdam 2020 are here!",
          body:
            "First of all, lets congratulate Kia King Ishii on joining the Vue.js core team! 🎉 He has been doing an incredible job building vuex-orm and will now focus on working on the next versions of Vuex.\n\nSpeaking of which – Vuex v4.0.0-alpha.1 has just been released! This is the version of Vuex that will work with Vue 3.0 but keep the familiar API you know from the current version.",
          sentAt: "2020-03-18T18:25:43.511Z",
          archived: false,
          read: false,
        },
        {
          id: 4,
          from: "anthony@vuejsdevelopers.com",
          subject:
            "'Vue 3 Release Roadmap' + 6 more must-read articles from this week",
          body: "Newsletter Issue #161",
          sentAt: "2020-03-24T18:25:43.511Z",
          archived: true,
          read: false,
        },
      ],
    };
  },
  computed: {
    unArchivedEmails() {
      return this.emails
        .reduce((acc, emails) => {
          acc.push(emails);
          return acc;
        }, [])
        .sort((elem1, elem2) => (elem1.sentAt < elem2.sentAt ? 1 : -1))
        .filter((e) => !e.archived);
    },
  },
  methods: {
    sortEmail(email) {
      return email.sort((elem1, elem2) =>
        elem1.sentAt < elem2.sentAt ? 1 : -1
      );
    },
  },
};
</script>

<style scoped lang="scss"></style>
