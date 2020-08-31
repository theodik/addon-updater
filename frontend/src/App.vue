<style scoped>
.footer {
  background-color: rgba(0,0,0,0)
}

.break-word {
  word-break: break-word;
}
</style>

<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <v-layout column>
          <v-layout>
            <v-card v-for="(ext, i) in extensions" :key="`ext-${i}`" height="130" width="130" class="mr-5" @click="extSelected = i">
              <v-card-title class="justify-center text-uppercase break-word">{{ext.name}}</v-card-title>
              <v-footer absolute padless tile class="v-card__text rounded-b footer pl-2">
                {{ ext.date || ext.version }}
              </v-footer>
            </v-card>
          </v-layout>
          <v-layout class="mt-5">
            <v-window v-model="extSelected">
              <v-window-item v-for="(ext, i) in extensions" :key="`ext-settings-${i}`">
                <v-card width="100vw">
                  <v-card-title>{{ext.name}}</v-card-title>
                  <v-card-text>
                    <div>Date: {{ ext.date }}</div>
                    <div>Version: {{ ext.version }}</div>
                  </v-card-text>
                  <v-card-actions>
                    <template v-if="!ext.installed">
                      <v-btn depressed @click="extensions[i].installed = true">
                        Install
                      </v-btn>
                    </template>
                    <template v-else>
                      <v-btn depressed @click="extensions[i].installed = false">
                        Uninstall
                      </v-btn>
                      <v-btn depressed>
                        Update
                      </v-btn>
                    </template>
                  </v-card-actions>
                </v-card>
              </v-window-item>
            </v-window>
          </v-layout>
        </v-layout>
      </v-container>
      <v-footer app>
        <v-layout class="my-3">
          <v-layout column class="mr-5">
            <div>{{ process.progress }}% {{ process.title }} {{ process.current }}/{{ process.total }}</div>
            <v-progress-linear height="10" :value="process.progress"></v-progress-linear>
          </v-layout>

          <v-btn height="60" width="150" color="primary">Play</v-btn>
        </v-layout>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      extensions: [
        {
          name: "arcdps",
          version: new Date("2020-08-29 16:16").toLocaleDateString(),
          date: new Date("2020-08-29 16:16").toLocaleDateString(),
          installed: true,
        },
        {
          name: "Boon Table",
          version: "v2.0.0-alpha",
          date: new Date("27 Dec 2019").toLocaleDateString(),
          installed: false,
        },
        {
          name: "Radial",
          version: "v2.0.0-alpha",
          date: new Date("20 Jul 2020").toLocaleDateString(),
          installed: false,
        },
        {
          name: "Taco",
          version: "047.2802r",
          date: null,
          installed: false,
        },
      ],
      process: {
        working: true,
        title: "Updating arcdps",
        current: 1,
        total: 3,
        progress: 31,
      },
      extSelected: 0,
    }),
    props: {
      source: String
    }
  }
</script>

<style>
  .logo {
    width: 16em;
  }
</style>
