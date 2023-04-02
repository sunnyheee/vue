<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" v-on:click="addTodo">
      <i>+</i>
    </span>
    <AlertModal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        warning!
        <span class="closeModalBtn" @click="showModal = false">X</span>
      </h3>
      <div slot="body">You haven't entered anything</div>
    </AlertModal>
  </div>
</template>

<script>
import AlertModal from "./common/AlertModal.vue";

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      console.log(this.newTodoItem);
      // save

      if (this.newTodoItem !== "") {
        this.$emit("addTodoItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this, (this.newTodoItem = "");
    },
  },
  components: {
    AlertModal,
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  width: 80%;
}
.inputBox span i {
  font-size: 3rem;
  color: #fff;
  display: flex;
  justify-content: center;
  font-weight: bold;
  font-style: normal;
  cursor: pointer;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
}
</style>
