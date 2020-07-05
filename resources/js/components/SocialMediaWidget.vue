<template>

    <widget :meta="meta">

        <template v-slot="{ value, loading }">

            <div :style="{ backgroundColor: icon.color }"
                 class="flex flex-1 justify-center items-center h-full relative rounded-t-lg flex-1">

                <component :is="icon.component" class="text-white absolute"/>

                <TestChart class="absolute w-full h-full"/>

            </div>

            <div style="background: #23242d" class="flex text-white justify-center rounded-b-lg p-2"
                 :class="{ 'p-4': meta.h > 1 }">

                <template v-for="([ content, label ], index) of value">

                    <div v-if="index > 0" class="social-media-widget__divider border-r mx-2"></div>

                    <div :key="index" class="flex text-center flex-col p-1">
                        <div class="font-normal text-2xl leading-normal">{{ content }}</div>
                        <div class="text-xs uppercase">{{ label }}</div>
                    </div>

                </template>

            </div>

        </template>

    </widget>

</template>

<script>

    import Facebook from './icons/Facebook'
    import Twitter from './icons/Twitter'
    import TestChart from './TestChart'

    const socialMedias = {
        facebook: {
            component: Facebook,
            color: '#3b5998'
        },
        twitter: {
            component: Twitter,
            color: '#00acee'
        }
    }

    export default {
        props: [ 'meta' ],
        components: { TestChart },
        data() {
            return {
                socialMedias
            }
        },
        computed: {
            icon() {
                return socialMedias[ this.meta.options.type ]
            }
        }
    }

</script>


<style>

    .social-media-widget__divider {
        border-color: rgba(0, 0, 21, .2);
    }

</style>
