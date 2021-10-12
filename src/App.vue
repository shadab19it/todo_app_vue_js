<template>
  <div>
    <v-app id="inspire">
      <v-app-bar app>
        <div class="header_title">
          <v-avatar color="primary" size="50" v-if="userName">
            <div class="user_avatar">
              {{ userName[0].toUpperCase() }}
            </div>
          </v-avatar>
          <v-toolbar-title class="user_name" v-if="userName">
            {{ userName }}
          </v-toolbar-title>
        </div>
      </v-app-bar>

      <v-main>
        <div class="main_container" v-if="userName">
          <v-container class="todo_container">
            <v-row align="center">
              <!-- todo Header -->
              <v-col>
                <div class="toto_title">
                  Set Your Task for Today
                </div>
              </v-col>
            </v-row>

            <!-- todo input box -->
            <v-row align="start" justify="cetenr">
              <v-col cols="10"> <v-text-field v-model="todo_text" label="todo..." solo></v-text-field></v-col>
              <v-col cols="2">
                <v-btn color="primary" class="add_btn" @click="onClickAddTodo" elevation="2">Add</v-btn>
              </v-col>
            </v-row>

            <!-- toto list -->
            <v-list dense>
              <v-list-item-group color="primary">
                <transition-group
                  enter-active-class="animate__animated animate__bounceIn"
                  leave-active-class="animate__animated animate__bounceOut"
                >
                  <v-list-item v-for="(todo, i) in todos" :key="i">
                    <v-list-item-content>
                      <v-list-item-title v-text="todo.text"></v-list-item-title>
                    </v-list-item-content>
                    <v-list-item-icon @click="deleteTodo(i)">
                      <v-icon v-text="icon.mdiDelete"></v-icon>
                    </v-list-item-icon>
                  </v-list-item>
                </transition-group>
              </v-list-item-group>
            </v-list>
          </v-container>
        </div>
        <!--  -->
      </v-main>

      <!-- User Name dialog -->

      <v-dialog v-model="userInputDialog" persistent max-width="500px">
        <v-card>
          <v-card-title>
            <span>Hi, Enter your Name and Set Today Task</span>
          </v-card-title>
          <v-card-text>
            <v-text-field v-model="inputField" placeholder="Enter Your Name" label="Enter Your Name"></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" text @click="closeDialog">
              Enter
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-app>
  </div>
</template>

<script>
  // eslint-disable-next-line no-unused-vars
  import { mdiDelete } from "@mdi/js";
  export default {
    data: () => ({
      icon: {
        mdiDelete,
      },
      drawer: null,
      userInputDialog: true,
      userName: "",
      inputField: "",
      todo_text: "",
      todos: [],
    }),
    methods: {
      closeDialog() {
        if (!this.inputField) return;
        this.userInputDialog = false;
        this.userName = this.inputField;
      },

      onClickAddTodo() {
        if (this.todo_text) {
          this.todos.push({ text: this.todo_text, status: "to_do" });
          this.todo_text = "";
        }
      },
      deleteTodo(id) {
        this.todos.splice(id, 1);
      },
    },
  };
</script>

<style scoped>
  .header_title {
    display: flex;
    align-items: center;
  }
  .user_name {
    margin-left: 10px;
  }
  .user_avatar {
    font-size: 1.3rem;
    color: #fff;
  }
  .toto_title {
    margin-top: 20px;
    font-size: 2.5rem;
    text-align: center;
  }
  .main_container {
    max-height: auto;
    width: 100%;
    display: flex;
    place-items: center;
  }

  .add_btn {
    margin-top: 5px;
  }

  .todo_container {
    max-width: 500px;
  }
</style>
