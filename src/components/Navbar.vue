<template>
  <div class="navbar bg-base-100 shadow-md px-8 fixed top-0 left-0 z-[99999]">
    <div class="navbar-start">
      <div class="dropdown">
        <label tabindex="0" class="cursor-pointer lg:hidden">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h8m-8 6h16"
            />
          </svg>
        </label>
        <ul
          tabindex="0"
          class="menu menu-sm dropdown-content mt-8 z-[1] p-2 shadow bg-base-100 rounded-box w-52"
        >
          <li>
            <router-link class="hover:text-white hover:bg-rose-500" :to="{ name: 'byName' }">Search Meals</router-link>
          </li>
          <li>
            <router-link class="hover:text-white hover:bg-rose-500" :to="{ name: 'byLetter' }"
              >Meals By Letter</router-link
            >
          </li>
          <li>
            <router-link class="hover:text-white hover:bg-rose-500" :to="{ name: 'ingredients' }"
              >Meals By Ingredients</router-link
            >
          </li>
        </ul>
      </div>
      <router-link :to="{ name: 'home' }" class="text-lg sm:text-xl ml-3 font-semibold text-rose-500"
        ><img
          src="/hamburger.svg"
          alt="Icon"
          class="inline-block w-9 sm:w-10"
        />
        Meals
      </router-link>
    </div>
    <div class="navbar-center hidden lg:flex">
      <ul class="menu menu-horizontal px-1">
        <li>
          <router-link class="hover:text-white hover:bg-rose-500" :to="{ name: 'byName' }">Search Meals</router-link>
        </li>
        <li>
          <router-link class="hover:text-white hover:bg-rose-500" :to="{ name: 'byLetter' }">Meals By Letter</router-link>
        </li>
        <li>
          <router-link class="hover:text-white hover:bg-rose-500" :to="{ name: 'ingredients' }"
            >Meals By Ingredients</router-link
          >
        </li>
      </ul>
    </div>
    <div class="navbar-end">
      <a
        href="https://www.themealdb.com/api.php"
        target="_blank"
        class="px-3 py-2 sm:px-4 sm:py-2 bg-rose-500 rounded-lg text-xs sm:text-sm text-white"
        >API Docs</a
      >
    </div>
  </div>
</template>
