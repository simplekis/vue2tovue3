<!-- eslint-disable prettier/prettier -->
<template>
  <div>
    <select @change="updateSalutation">
      <option value="">-</option>
      <option
        v-for="item in salutations"
        :key="item"
        :value="item"
        :selected="salutation === item"
      >
        {{ item }}
      </option>
    </select>
    <input @input="updateName" :value="name" type="text" />
  </div>
</template>

<script>
const salutations = ["Ms.", "Mrs.", "Miss", "Mr.", "Dr."];
export default {
  props: {
    salutation: {
      type: String,
      default: "",
    },
    salutationModifiers: {
      default: () => ({}),
    },
    name: {
      type: String,
      default: "",
    },
    nameModifiers: {
      default: () => ({}),
    },
  },
  setup(props, { emit }) {
    const updateSalutation = (event) => {
      let val = event.target.value;
      if (props.salutationModifiers.capitalize) {
        val = val.toUpperCase();
      }
      emit("update:salutation", val);
    };
    const updateName = (event) => {
      let val = event.target.value;
      if (props.nameModifiers.capitalize) {
        val = val.charAt(0).toUpperCase() + val.slice(1);
      }
      emit("update:name", val);
    };
    return { salutations, updateSalutation, updateName };
  },
};
</script>

<style lang="scss" scoped>
div {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

select {
  margin-right: 0.5rem;
}
input {
  width: 50%;
}
</style>
