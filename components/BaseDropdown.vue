<template>
  <div class="base-dropdown">
    <button
      ref="showInputButton"
      class="custom-drop"
      @click="popperClickEvent"
    >
      Dropdown button ▼
    </button>
    <transition name="slide-fade">
      <div
        ref="dropdown"
        v-show="show"
        class="popover-custom"
      >
        <slot></slot>
      </div>
    </transition>
  </div>
</template>
<script>
    import Popper from 'popper.js'

    export default {
        props: {
            target: Object,
            show: Boolean,
            closeOutside: Boolean
        },
        data: () => ({
            button: null,
            dropdown: null
        }),
        mounted() {
            this.button = this.$refs.showInputButton;
            this.dropdown = this.$refs.dropdown;
            if (this.closeOutside) {
                this.setCloseOutside();
            }
        },
        methods: {
            popperClickEvent() {
                this.$emit('toggleDropdownContent');
                const popper = new Popper(this.button, this.dropdown, {
                    placement: 'auto',
                    modifiers: {
                        offset: {
                            offset: "0,5"
                        }
                    }
                });
            },
            setCloseOutside() {
                window.addEventListener('click', (e) => {
                    if (!e.target.classList.contains("custom-drop") && this.show === true) {
                        this.$emit('toggleDropdownContent');
                    }
                })
            }
        },
        beforeDestroy() {
            window.removeEventListener('click');
        }
    }
</script>
<style scoped lang="scss">
  .base-dropdown {
    position: relative;
    background-color: orange;

    .custom-drop {
      width: 100%;
      font-weight: 400;
      color: #212529;
      border: 1px solid dimgray;
      text-align: center;
      vertical-align: middle;
      background-color: transparent;
      padding: .375rem .75rem;
      font-size: 1rem;
      line-height: 1.5;
      border-radius: .25rem;

      &:focus {
        outline: none;
        border: 1px solid orangered;
        transition: 1s ease;
      }
    }

    .popover-custom {
      width: 100%;
      display: block;
      padding: 0;
      border: 1px solid dimgray;
      max-height: 300px;
      overflow: auto;

      :nth-child(even) {
        background-color: lightblue;
      }
    }

    .popover-custom::-webkit-scrollbar {
      display: none;
    }

    .popover-custom {
      -ms-overflow-style: none; /* IE and Edge */
      scrollbar-width: none; /* Firefox */
    }
  }

  .slide-fade-enter-active {
    transition: all .8s ease;
  }

  .slide-fade-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }

  .slide-fade-enter, .slide-fade-leave-to
    /* .slide-fade-leave-active до версии 2.1.8 */
  {
    opacity: 0;
  }
</style>

