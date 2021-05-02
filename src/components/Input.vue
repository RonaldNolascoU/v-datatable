<template>
  <div :class="width">
    <div class="mt-1 relative rounded-md shadow-sm">
      <div
        class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none"
      ></div>
      <input
        type="text"
        class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-3 pr-12 sm:text-sm border-gray-300 rounded-md"
        :value="value"
        @blur="saveField($event.target.value)"
        @keydown="onKeyDown"
      />
    </div>
  </div>
</template>

<script>
export default {
    props: {
        width: {
            default: 'w-1/2'
        },
        field: String,
        value: String
    },
    methods: {
        onKeyDown(event) {
            switch (event.which) {
                case 13:  //Enter
                    this.saveField(event.target.value)
                break;

                case 9: //Tab
                    this.saveField(event.target.value)
            }
        },
        saveField(value) {
            //Updating prop value
            this.$emit('update:value', value)
        }
    }
};
</script>

<style>
</style>