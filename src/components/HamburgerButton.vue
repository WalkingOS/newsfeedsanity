<template>
    <div
        class="menu-toggle absolute top-4 left-4 w-8 h-8 cursor-pointer z-50"
        :class="menu_is_active ? 'is-active' : ''"
        @click="ToggleMenu"
    >
        <div class="hamburger absolute top-1/2 left-1/2 w-8 h-8">
            <span class="absolute top-1/2"></span>
        </div>
    </div>
</template>
<script>

import { computed } from 'vue'
import { useStore } from 'vuex'

export default {
    setup () {
        const store = useStore()

        const ToggleMenu = () => {
            store.dispatch('ToggleMenu')
        }

        return {
            menu_is_active: computed(() => store.state.menu_is_active),
            ToggleMenu
        }
    }
}
</script>

<style scoped>

    .hamburger {
        transform: translate(-50%, -50%);
    }

    .hamburger span,
    .hamburger span::before,
    .hamburger span::after {
        position: absolute;
        width: 100%;
        height: 4px;
        border-radius: 99px;
        background: white;
        transition: all 0.3s ease-in-out;
    }

    .hamburger span::before,
    .hamburger span::after {
        content: "";
    }

    .hamburger span::before {
        top: -8px;
    }
    .hamburger span::after {
        top: 8px;
    }

    .menu-toggle.is-active .hamburger > span {
        transform: rotate(45deg);
    }

    .menu-toggle.is-active .hamburger > span:before {
        top: 0;
        transform: rotate(0deg);
    }

    .menu-toggle.is-active .hamburger > span:after {
        top: 0;
        transform: rotate(90deg);
    }
    
</style>
