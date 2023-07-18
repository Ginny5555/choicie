<template>
  <div class="functions">
    <div class="users">
      <div class="custom-container">
        <div class="row mx-auto w-100 d-flex justify-content-center align-items-center">
          <div class="col-12 d-flex justify-content-center">
            <h1>Users list</h1>
          </div>
          <div class="col-lg-6 col-md-6 col-sm-12">
            <h2 class="text-center">To update user information just tap in information item</h2>
          </div>
          <div class="users-table col-lg-6 col-md-6 col-sm-12">
            <tbody>
              <tr v-for="user in users" :key="user.id">
                <!-- <td>{{ user.id }}</td> -->
                <td>
                  <input
                    type="text"
                    v-model="user.name"
                    @enter="updateUser(user.id, { field: 'name', value: user.name })"
                  />

                  <input
                    type="email"
                    v-model="user.email"
                    @enter="updateUser(user.id, { field: 'email', value: user.email })"
                  />
                </td>
                <td>
                  <button class="delete" @click="deleteUser(user.id)">Delete</button>
                  <button class="update" @click="updateUser(user.id,[ { field: 'name', value: user.name } , { field: 'email', value: user.email }])">Update</button>
                </td>
              </tr>
            </tbody>
          </div>
        </div>
      </div>
    </div>
    <div class="form">
      <div class="custom-container">
        <div class="row w-100">
          <div class="col-lg-6 col-md-6 col-sm-12">
            <form @submit.prevent="createUser">
              <div class="form-group">
                <label for="userName">Name:</label>
                <input type="text" class="form-control" id="userName" v-model="newUser.name" />
              </div>
              <div class="form-group">
                <label for="userEmail">Email:</label>
                <input type="email" class="form-control" id="userEmail" v-model="newUser.email" />
              </div>
              <button type="submit" class="success">Create User</button>
            </form>
          </div>
          <div class="col-lg-6 col-md-6 col-sm-12">
            <h2>Fill the textfield and press button</h2>
          </div>
        </div>
      </div>
    </div>
    <FooterView />
  </div>
</template>

<script>
import axios from "axios";
import FooterView from "@/components/FooterView.vue";

export default {
  name: "ApiReq",
  components: {
    FooterView
  },
  data() {
    return {
      users: [],
      newUser: {
        name: "",
        email: ""
      },
      userId: 0
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then(response => {
          this.users = response.data;
          console.log(response.data);
        })
        .catch(error => {
          console.error("Error:", error);
        });
    },
    deleteUser(userId) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/users/${userId}`)
        .then(() => {
          this.users = this.users.filter(user => user.id !== userId);
        })
        .catch(error => {
          console.error("Error:", error);
        });
    },

    createUser() {
      axios
        .post("https://jsonplaceholder.typicode.com/users", this.newUser)
        .then(response => {
          console.log("Created user:", response.data);
          this.users.push(response.data);
          this.newUser.name = "";
          this.newUser.email = "";
        })
        .catch(error => {
          console.error("Error:", error);
        });
    },

updateUser(userId, updatedFields) {
  // Ensure updatedFields is an array and has valid objects
  if (!Array.isArray(updatedFields) || updatedFields.length === 0) {
    console.error('Invalid updatedFields array:', updatedFields);
    return;
  }

  // Create an object with all the updated fields and their values
  const updatedUser = {};
  for (const fieldUpdate of updatedFields) {
    if (fieldUpdate.field && fieldUpdate.value) {
      updatedUser[fieldUpdate.field] = fieldUpdate.value;
    }
  }

  axios
    .put(
      `https://jsonplaceholder.typicode.com/users/${userId}`,
      updatedUser
    )
    .then(response => {
      console.log("Updated user:", response.data);
      const updatedIndex = this.users.findIndex(user => user.id === userId);
      if (updatedIndex !== -1) {
        // Update each field in the user object
        for (const fieldUpdate of updatedFields) {
          if (fieldUpdate.field && fieldUpdate.value) {
            this.users[updatedIndex][fieldUpdate.field] = fieldUpdate.value;
          }
        }
      }
    })
    .catch(error => {
      console.error("Error:", error);
    });
}

  }
};
</script>
<style lang="scss" scoped>
@import "../assets/styles.scss";
input {
  border: none;
}
td {
  border-bottom: 1px solid $text-grey;
  padding: 24px 0;
}
.users {
  padding: 70px 0;
  background: $bg-dark;
  & h1 {
    color: $white;
  }
  & h2 {
    color: $purple-nav;
  }
  & input {
    padding: 16px;
    border-radius: 50px;
    background: transparent;
    color: white;
    font-size: 18px;
    &:hover {
      border: none;
    }
  }
  &-table {
    border: 1px solid $text-grey;
    border-radius: 20px;
    padding: 16px;
  }
}

.form {
  padding: 70px 0;
  background: $yellow-light;
  width: 100%;
  margin: 0;
  & h2 {
    color: $text-color;
  }
  & input {
    padding: 16px;
    border-radius: 50px;
    width: 288px;
    color: $black;
    font-size: 18px;
    border: 1px solid $brand-yellow;
  }
}
button {
  color: $white;
  border: none;
  font-size: 14px;
  padding: 12px;
  width: 100px;
  border-radius: 50px;
  margin-bottom: 10px;
  &.delete {
    background: $text-danger;
    &:hover {
      background: $danger-hover;
    }
  }
  &.update {
    background: $brand-yellow;
    &:hover {
      background: $yellow-focus;
    }
  }
  &.success {
    background: $drpurple-nav;
    width: 100%;
    width: 288px;
    &:hover {
      background-color: $purple-focus;
    }
    &:focus {
      background-color: $purple-focus;
    }
    &:disabled {
      background: $purple-disabled;
      color: $drpurple-nav;
    }
  }
}

@media screen and (min-width: 320px) and (max-width: 767px) {
  .users {
    padding: 40px 0;
    & input {
      padding: 14px;
      font-size: 14px;
    }

    & h1 {
      font-size: 24px;
      margin-bottom: 16px;
    }
    & h2 {
      font-size: 16px;
      line-height: 24px;
      margin-bottom: 16px;
    }
  }
  .form {
    & h2 {
      font-size: 16px;
      line-height: 24px;
      margin-bottom: 16px;
      margin: 0 auto;
    }

    margin: 0 auto;
    display: flex;
    justify-content: center;
  }
}
@media screen and (min-width: 768px) and (min-width: 768px) {
  .users {
    padding: 40px 0;
    & input {
      padding: 14px;
      font-size: 14px;
    }

    & h1 {
      font-size: 24px;
      margin-bottom: 16px;
    }
    & h2 {
      font-size: 16px;
      line-height: 24px;
      margin-bottom: 16px;
    }
  }
  .form {
    margin: 0 auto;
    display: flex;
    justify-content: center;
    & form {
      margin: 0 auto;
    }
  }
}
</style>