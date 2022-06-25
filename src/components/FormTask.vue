<template>
  <div
    class="flex items-center justify-center space-x-10 w-11/12 mx-auto bg-slate-400"
  >
    <form @submit.prevent="addToForm" class="flex flex-col gap-10">
      <input
        type="text"
        class="pl-2"
        placeholder="label"
        v-model="form[index].label"
      />
      <input
        type="text"
        class="pl-2"
        placeholder="placeholder"
        v-model="form[index].placeholder"
      />
      <select v-model="form[index].type">
        <option value="input">input</option>
        <option value="textarea">textarea</option>
        <option value="date">date</option>
      </select>
      <button>Add to form</button>
    </form>
    <form v-show="inputGroup.length" @submit.prevent="handleSubmit">
      <div v-for="(item, index) in inputGroup" :key="index">
        <div v-if="item.type === 'textarea'">
          <label :for="item.label">{{ item.label }}</label>
          <textarea
            :id="item.label"
            :placeholder="item.placeholder"
            :name="item.label"
            cols="10"
            rows="10"
            class="resize-none"
            @input="handleChange($event, index)"
          ></textarea>
        </div>
        <div v-else>
          <label :for="item.label">{{ item.label }}</label>
          <input
            :type="item.type"
            :placeholder="item.placeholder"
            :name="item.label"
            :id="item.label"
            @input="handleChange($event, index)"
          />
        </div>
      </div>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import { reactive, ref } from "@vue/reactivity";
export default {
  name: "FormTask",
  setup() {
    const index = ref(0);
    const inputGroup = ref([]);
    const form = reactive([
      {
        label: "",
        placeholder: "",
        type: "",
      },
    ]);
    const group = reactive([]);
    const addToForm = () => {
      index.value++;
      let newForm = [...form];
      newForm.slice(-1, 1);
      inputGroup.value = [...newForm];
      form.push({
        label: "",
        placeholder: "",
        type: "",
      });
      group.push({
        label: "",
        value: "",
      });
    };
    const handleChange = (e, index) => {
      const { value, name } = e.target;
      group[index].label = name;
      group[index].value = value;
    };
    const handleSubmit = () => {
      alert(JSON.stringify(group, null, 2));
    };
    return {
      form,
      group,
      addToForm,
      handleChange,
      index,
      inputGroup,
      handleSubmit,
    };
  },
};
</script>
