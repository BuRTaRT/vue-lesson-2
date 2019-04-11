<template>
  <div class="wrapper">
    <div class="sample">
      <form v-if="status">
        <div class="progress">
          <div class="progress-bar" :style="progress"></div>
        </div>
        <div>
          <div class="form-group" v-for="(item, index) in info">
            <label>{{ item.name }}</label>
            <i v-if="item.bool" :class="item.class"></i>
            <input
              v-on:input="reverseBool(index)"
              v-model="item.value"
              type="text"
              class="form-control"
            />
          </div>
        </div>
        <button @click="status=!status"
          :disabled="btnDisabled"
          class="btn btn-primary"
          @click.prevent=""
        >
          Send Data
        </button>
      </form>
      <div>
        <table v-if="!status" class="table table-bordered">
          <tr v-for="item in info">
            <td>{{item.name}}</td>
            <td>{{item.value}}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      status:true,
      accept: "fas fa-check-circle",
      decline: "fas fa-exclamation-circle",
      btnDisabled: true,
      info: [
        {
          name: "Name",
          value: "",
          pattern: /^[a-zA-Z ]{2,30}$/,
          bool: false,
          class: ""
        },
        {
          name: "Phone",
          value: "",
          pattern: /^[0-9]{7,14}$/,
          bool: false,
          class: ""
        },
        {
          name: "Email",
          value: "",
          pattern: /.+/,
          bool: false,
          class: ""
        },
        {
          name: "Some Field 1",
          value: "",
          pattern: /.+/,
          bool: false,
          class: ""
        },
        {
          name: "Some Field 2",
          value: "",
          pattern: /.+/,
          bool: false,
          class: ""
        }
      ]
    };
  },
  methods: {
    reverseBool(index) {
      if (this.info[index].value != "") {
        this.info[index].bool = true;
      } else if (this.info[index].value == "") {
        this.info[index].bool = false;
      }
      if (this.info[index].pattern.test(this.info[index].value)) {
        this.info[index].class = this.accept;
      } else if (!this.info[index].pattern.test(this.info[index].value)) {
        this.info[index].class = this.decline;
      }
    }
  },

  computed: {
    progress() {
      let n = 0;
      let numberOfInputs = this.info.length;
      for (let item in this.info) {
        if (this.info[item].class == "fas fa-check-circle") {
          n++;
        }
      }
      if (n == this.info.length) {
        this.btnDisabled = false;
      }
      return `width:${(100 / numberOfInputs) * n}%;`;
    }
  }
};
</script>

<style>
.wrapper {
  padding-top: 20px;
}
h3 {
  cursor: pointer;
}
.sample {
  width: 35%;
  margin: 0 auto;
}
.fa-exclamation-circle {
  color: red;
}
.fa-check-circle {
  color: green;
}
</style>
