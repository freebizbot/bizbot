<template>
    <div aria-live="assertive" class="pointer-events-none fixed top-20 inset-0 flex items-end px-4 py-6 sm:items-start sm:p-6">
        <div class="flex w-full flex-col items-center space-y-4 sm:items-end">
            <!-- Notification panel, dynamically insert this into the live region when it needs to be displayed -->
            <transition enter-active-class="transform ease-out duration-300 transition" enter-from-class="translate-y-2 opacity-0 sm:translate-y-0 sm:translate-x-2" enter-to-class="translate-y-0 opacity-100 sm:translate-x-0" leave-active-class="transition ease-in duration-100" leave-from-class="opacity-100" leave-to-class="opacity-0">
                <div v-if="show" :class="color" class="pointer-events-auto w-full max-w-sm overflow-hidden rounded-lg shadow-lg ring-1 ring-black ring-opacity-5">
                    <div class="p-4">
                        <div class="flex items-center">
                            <div class="flex w-0 flex-1 justify-between">
                                <p class="w-0 flex-1 text-sm font-medium text-gray-900">{{title}}</p>
                            </div>
                            <div class="ml-4 flex flex-shrink-0">
                                <button type="button" @click="show = false" class="inline-flex rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                                    <span class="sr-only">Close</span>
                                    <XMarkIcon class="h-5 w-5" aria-hidden="true" />
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </transition>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { XMarkIcon } from '@heroicons/vue/20/solid'
</script>

<script>
export default {
    props: {
        title: {
            type: String,
            default: 'Notification'
        },
        type: {
            type: String,
            default: 'success'
        }
    },
    data() {
        return {
            show: true,
        }
    },
    computed: {
        color() {
            switch (this.type) {
                case 'success':
                    return 'bg-green-50 border-green-400 text-green-700';
                case 'error':
                    return 'bg-red-50 border-red-400 text-red-700';
                case 'warning':
                    return 'bg-yellow-50 border-yellow-400 text-yellow-700';
                case 'info':
                    return 'bg-blue-50 border-blue-400 text-blue-700';
                default:
                    return 'bg-green-50 border-green-400 text-green-700';
            }
        }
    },
    mounted() {
        setTimeout(() => {
            this.show = false
        }, 2300)
    }
}
</script>
