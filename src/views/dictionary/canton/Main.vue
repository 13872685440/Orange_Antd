<template>
  <div>
    <s-list v-if="currentTab === 'list'" :searchCode="searchCode" @edit="edit" @search="search" />
    <s-form
      v-if="currentTab === 'add'"
      :formId="id"
      :type="type"
      @edit="edit"
    />
  </div>
</template>

<script>
import SList from "./List";
import SForm from "./Form";

export default {
  name: "Main_Canton",
  components: {
    SList,
    SForm
  },
  data() {
    return {
      currentTab: "list",
      id: "",
      type: "",
      searchCode: ""
    };
  },
  methods: {
    edit(data) {
      this.currentTab = data.state;
      this.id = data.id;
      this.type = data.type;
    },
    search(value) {
      this.searchCode = value;
    }
  }
};
</script>
