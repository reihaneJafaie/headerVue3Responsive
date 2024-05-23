<template>
  <section class="relative ">
    <header
      class="mt-6 mb-20 bg-white relative rounded-full shadow-lg py-3"
      dir="rtl"
    >
      <nav class="flex justify-between items-center px-3">
        <div class="flex gap-x-8 items-center">
          <img src="./assets/images/1.png" class="w-[100px] rounded-full" alt="">
          <ul class="flex gap-x-2 md:ullist">
            <li v-for="item in menu" class="items text-nowrap px-4 py-2">
              <router-link :to="item.route" class="text-sm">{{
                item.title
              }}</router-link>

              <ul
                v-if="item.child && item.child.length"
                class="rounded-lg subMenu border bg-white"
              >
                <li v-for="child in item.child" class="itemChild">
                  <RouterLink to="/" class="block py-2 px-10">{{
                    child.title
                  }}</RouterLink>
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <div class="ml-5">
          <router-link to="/login-dr">
            <button class="hidden md:block btnRaRa text-nowrap	"> Login / signin</button>
          </router-link>

          <button
            @click="toggleMenu"
            type="button"
            class="hamberger mx-2 text-black hover:text-gray-400 focus:outline-none focus:text-gray-400"
          >
            <svg viewBox="0 0 24 24" class="w-6 h-6 fill-current">
              <path
                fill-rule="evenodd"
                d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
              ></path>
            </svg>
          </button>
        </div>
      </nav>
    </header>
    <Menu @activity="activity" :class="{ open: showMenu, close: !showMenu }" ></Menu>
  </section>
</template>
<style>
.items {
  @apply text-gray-950 font-bold text-base;
}
</style>

<script setup>
import { ref } from "vue";
// import logo from "@/components/shared/Logo.vue";
import Menu from "../src/components/menu.vue";

let showMenu = ref(false);
function activity(activ) {
  showMenu.value = activ;
}
function toggleMenu() {
  showMenu.value = true;
}
let menu = [
  {
    id: 1,
    title: "Home",
    route: "/",
  },
  {
    id: 2,
    title: "Doctors",
    route: "/list-doctor",
    // child: [
    //   {
    //     title: "پوست",
    //   },
    //   {
    //     title: "آلرژی",
    //   },
    //   {
    //     title: "تغذیه",
    //   },
    // ],
  },
  {
    id: 3,
    title: "Weblogs",
    route: "/weblogs",
  },
  {
    id: 4,
    title: "FAQ",
    route: "/faq",
  }
];
</script>

<style scoped>
.open {
  transform: translateX();
}

.itemChild:hover {
  background-color: #c0d9ff52;
  transition: 0.25;
}

.subMenu {
  display: none;
  position: absolute;
  top: 70%;
}
.items:hover .subMenu {
  display: block;
}

/* Hide .hamberger in Windows */
@media (min-width: 768px) {
  .hamberger {
    display: none;
  }
}

/* Move .ullist below nav in mobile */
@media (max-width: 767px) {
  .md\:ullist {
    display: none;
  }
}
</style>

