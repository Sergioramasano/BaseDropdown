<template>
  <section
    ref="parent"
    class="container"
  >
    <BaseDropdown
      :target="this.$refs"
      :show.sync="show"
      :closeOutside="closeOutside"
      @toggleDropdownContent="show = !show"
    >
      <p
        v-for="(option, idx) in options"
        :key="idx"
        class="item"
      >
        {{option.value}}
      </p>
    </BaseDropdown>
    <BaseDropdown
      :target="this.$refs"
      :show.sync="show1"
      :closeOutside="closeOutside"
      @toggleDropdownContent="show1 = !show1"
    >
      <p
        v-for="(option, idx) in options"
        :key="idx"
        class="item"
      >
        {{option.value}}
      </p>
    </BaseDropdown>
  </section>
</template>

<script>
    import BaseDropdown from '~/components/BaseDropdown.vue'

    export default {
        components: {
            BaseDropdown
        },
        data: () => ({
            options: [
                {
                    value: "option 1"
                },
                {
                    value: "option 2"
                },
                {
                    value: "option 3"
                }
            ],
            show: false,
            show1: false,
            closeOutside: true
        })
    }
</script>

<style>
  .container {
    min-height: 100vh;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    text-align: center;
  }

  .item {
    padding-top: 10px;
    padding-bottom: 10px;
    box-sizing: border-box;
    background-color: palevioletred;
  }
</style>

