<template>
  <div>
    <s-entity
      :formId="formId"
      :taskId="taskId"
      :path="path"
      :readOnly="readOnly"
      @edit="edit"
      ref="sentity"
    >
      <span slot="process_button">
        <a-button style="margin-left: 8px" @click="edit">返回</a-button>
        <a-button
          style="margin-left: 8px"
          @click="$refs.shyj.add('审批通过','handleSubmitTG')"
          type="primary"
        >复审通过</a-button>
      </span>
    </s-entity>
    <s-shyj ref="shyj" @handleSubmitTG="handleSubmitTG"></s-shyj>
  </div>
</template>
<script>
import { editForm } from "@/utils/mixin";
import SEntity from "../Entity";
import SShyj from "@/components/Comment/SShyj";

export default {
  name: "Task_Form",
  components: {
    SEntity,
    SShyj
  },
  mixins: [editForm],
  data() {
    return {
      readOnly: true,
      formId: "",
      taskId: "",
      task_crtUid: ""
    };
  },
  beforeRouteEnter(to, from, next) {
    next(vm => {
      vm.formId = to.params.keyValue;
      vm.taskId = to.params.id;
      vm.task_crtUid = to.params.task_crtUid;
    });
  },
  created() {
    const prefix = "/" + this.GLOBAL.MODEL_SYSTEM;
    this.path.edit_path = prefix + "/test3/edit";
    this.path.save_path = prefix + "/test3/save";
    this.path.submit_path = prefix + "/process/countersign";
  },
  methods: {
    edit() {
      this.toHome();
    },
    handleSubmitTG(obj) {
      let data = {
        usermaps: {
          userId: this.task_crtUid,
          node: "会签"
        },
        shjl: "审批通过",
        shyj: obj.shyj,
        step: 2,
        processName: "测试流程3",
        service: "Test_Sq_Service",
        task_id: this.taskId,
        variables: {
          fushen: "复审通过"
        },
        node: "testacthq"
      };
      this.$refs.sentity.handleSubmitProcess_msg(data);
    }
  }
};
</script>
