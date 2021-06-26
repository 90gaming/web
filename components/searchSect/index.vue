<template>
    <section>
        <div class="max-w-3xl px-6 py-16 mx-auto text-center">
            <h1 class="text-3xl font-semibold text-gray-800 dark:text-gray-100">Search private server games</h1>
            <p class="max-w-md mx-auto mt-2 text-white dark:text-white-400">Gamer zone, Be careful.</p>

            <form class="flex flex-col mt-2 space-y-3 sm:space-y-0 sm:flex-row sm:justify-center sm:-mx-2" @submit.stop.prevent="submit">
                <input v-model="insearch" id="search" type="text" class="px-4 py-2 text-gray-700 bg-white border border-gray-300 rounded-md sm:mx-2 dark:bg-gray-800 dark:text-gray-300 dark:border-gray-600 focus:border-blue-500 dark:focus:border-blue-500 focus:outline-none focus:ring" placeholder="Search Private Server ...">
                
                <button type="submit" class="px-4 py-2 text-sm font-medium tracking-wide text-white capitalize transition-colors duration-200 transform bg-indigo-700 rounded-md sm:mx-2 hover:bg-indigo-600 focus:outline-none focus:bg-indigo-600">
                    Search
                </button>
            </form>
        </div>
    </section>
</template>
<script>
export default {
    data(){
        return{
            insearch:''
        }
    },
    methods:{
        submit(){
            this.$router.push("/search/"+this.insearch);
        }
    }
}
</script>