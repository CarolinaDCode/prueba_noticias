<template>
  <v-app>
    <v-main>
        <RouterView :key="$route.fullPath" />
    </v-main>
  </v-app>
</template>