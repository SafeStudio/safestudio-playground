<template>
  <div :class="['dropdown', show ? 'show' : '']">
    <button :class="['btn', `btn-${colorStyle}`, 'dropdown-toggle']" type="button" :id="`dropdown-${id}`" data-toggle="dropdown" aria-haspopup="true" :aria-expanded="show" @click="toggle">
      {{ selectedItemLabel.length > 0 ? selectedItemLabel : title }}
    </button>

    <div :class="['dropdown-menu', show ? 'show' : '']" :aria-labelledby="`dropdown-${id}`">
      <a v-for="(item, index) in items" :key="index" class="dropdown-item" @click="select(item)">{{ item.label }}</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'bootstrap-dropdown',
  props: {
    title: {
      type: String,
      required: true,
      default: ''
    },
    colorStyle: {
      type: String,
      default: 'primary'
    },
    items: {
      type: Array,
      required: true,
      default: () => {
        return [];
      }
    }
  },
  data() {
    return {
      id: Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15),
      show: false,
      selectedItemLabel: '',
    }
  },
  methods: {
    toggle() {
      this.show = !this.show;
    },
    select(item) {
      this.show = false;
      this.selectedItemLabel = item.label;
      this.$emit('value-selected', item.value);
    }
  }
}
</script>

