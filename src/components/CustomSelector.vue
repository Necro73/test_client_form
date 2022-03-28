<template>
    <div class="custom-select" :tabindex="tabindex" @blur="open = false">
        <div class="selected" :class="{ open: open }" @click="open = !open">
            {{ multiple ? (selectedMultiple.length==0 ? '(пусто)' : selectedMultiple.join(", ")) : selected }}
        </div>
        <div class="items" :class="{ selectHide: !open }">
            <div :class="{isSelected: checkSelectMultiple(option)}"
                 v-for="(option, i) of options"
                 :key="i"
                 @click="selectItem(option)"
            >
                {{ option }}
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        props: {
            options: {
                type: Array,
                required: true,
            },
            default: {
                type: String,
                required: false,
                default: null,
            },
            tabindex: {
                type: Number,
                required: false,
                default: 0,
            },
            multiple: {
                type: Boolean,
                required: false,
            }
        },
        data() {
            return {
                selected: this.default
                    ? this.default
                    : this.options.length > 0
                        ? this.options[0]
                        : null,
                selectedMultiple: [],
                open: false,
            };
        },
        mounted() {
            if (!this.multiple) {
                this.$emit("input", this.selected);
            }
        },
        methods: {
            selectItem(option) {
                if (this.multiple) {
                    if (this.selectedMultiple.includes(option)) {
                        this.selectedMultiple.splice(this.selectedMultiple.indexOf(option), 1);
                    } else {
                        this.selectedMultiple.push(option);
                    }
                    this.open = false;
                    this.$emit('input', this.selectedMultiple);
                    console.log(this.selectedMultiple);
                } else {
                    this.selected = option;
                    this.open = false;
                    this.$emit('input', option);
                }
            },
            checkSelectMultiple(option) {
                if (this.multiple) {
                    return this.selectedMultiple.includes(option);
                } else {
                    return false;
                }
            }
        },
    };
</script>

<style lang="scss" scoped>
    .custom-select {
        position: relative;
        width: 100%;
        text-align: left;
        outline: none;
        height: 47px;
        line-height: 47px;
    }

    .custom-select .selected {
        background-color: #ffffff;
        border-radius: 6px;
        border: 1px solid #ececec;
        color: #000000;
        padding-left: 1em;
        cursor: pointer;
        user-select: none;
    }

    .custom-select .selected.open {
        border: 1px solid #ececec;
        border-radius: 6px 6px 0px 0px;
    }

    .custom-select .selected:after {
        position: absolute;
        content: "";
        top: 22px;
        right: 1em;
        width: 0;
        height: 0;
        border: 5px solid transparent;
        border-color: #000000 transparent transparent transparent;
    }

    .custom-select .items {
        color: #000000;
        border-radius: 0px 0px 6px 6px;
        overflow: hidden;
        border-right: 1px solid #ececec;
        border-left: 1px solid #ececec;
        border-bottom: 1px solid #ececec;
        position: absolute;
        background-color: #ffffff;
        left: 0;
        right: 0;
        z-index: 1;
    }

    .custom-select .items div {
        color: #000000;
        padding-left: 1em;
        cursor: pointer;
        user-select: none;
    }

    .custom-select .items div:hover {
        background-color: #ececec;
    }

    .selectHide {
        display: none;
    }

    .isSelected {
       background-color: #888888 !important;
        color: #ffffff !important;
        &:hover {
            background-color: #ececec !important;
            color: #000000 !important;
        }
    }
</style>