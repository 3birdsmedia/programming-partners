<template>
    <div :class="classes">
        <slot />

        <div
            class="lines"
            @click="toggleMenu()"
        >
            <div class="line line-1" />
            <div class="line line-2" />
        </div>
    </div>
</template>

<script>
export default {
    props: {
        isOpened: {
            type: Boolean,
            default: false,
        },
    },
    computed: {
        classes() {
            return ["global-hamburger", { "is-opened": this.isOpened }]
        },
    },
    methods: {
        toggleMenu() {
            // Toggle menu state
            this.$emit("menu-opened", !this.isOpened)
        },
    },
}
</script>

<style lang="scss" scoped>
.global-hamburger {
    display: inline-flex;
    flex-direction: row;
    align-items: center;
    cursor: pointer;

    // Styles for slot
    .logo {
        height: auto;
        max-width: 150px;
        transition: width 0.4s var(--easing-authentic-motion);
    }

    .lines {
        position: relative;
        padding: 20px 30px;
        height: 20px;
        width: 30px;

        .line {
            height: 2px;
            width: 30px;
            background-color: var(--color-yellow);
            position: absolute;
            transform-origin: center right;
            transition: transform 0.4s var(--easing-authentic-motion);
            z-index: 10;
        }
        .line-1 {
            top: 25px;
        }
        .line-2 {
            bottom: 25px;
        }
    }

    // Opened state
    &.is-opened {
        .line-1 {
            transform: rotate(-45deg) translate(1px, -8px);
        }
        .line-2 {
            transform: rotate(45deg) translate(1px, 8px);
        }
    }

    // Breakpoints
    @media #{$lt-phone} {
        .logo {
            max-width: 100px;
        }

        .lines {
            padding: 20px;
        }
    }
}
</style>
