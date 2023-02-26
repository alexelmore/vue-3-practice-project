<template>
  <main>
    <user-list
      :users="activeUsersSetup"
      @list-projects="selectUserSetup"
    ></user-list>
    <projects-list :user="selectedUserSetup"></projects-list>
  </main>
</template>

<script>
import USER_DATA from "./dummy-data.js";
import { ref, reactive } from "vue";
import UserList from "./components/users/UserList.vue";
import ProjectsList from "./components/projects/ProjectsList.vue";

export default {
  components: {
    UserList,
    ProjectsList,
  },

  // Vue 3 Setup Method
  setup() {
    // Data properties
    const selectedUserSetup = ref(null);
    const activeUsersSetup = reactive(USER_DATA);

    // Methods
    function selectUserSetup(uid) {
      console.log("fired");
      selectedUserSetup.value = activeUsersSetup.find((usr) => usr.id === uid);
    }

    // Return properties in order to expose in the component template
    return { selectedUserSetup, activeUsersSetup, selectUserSetup };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}

main {
  display: flex;
  justify-content: space-around;
}

button {
  font: inherit;
  border: 1px solid #00006b;
  background-color: transparent;
  color: #00006b;
  padding: 0.5rem 1.5rem;
  cursor: pointer;
  margin: 0.5rem 0.5rem 0.5rem 0;
}
button:hover,
button:active {
  background-color: #efefff;
}

button.selected {
  background-color: #00006b;
  color: white;
}
</style>