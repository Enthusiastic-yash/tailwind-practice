<script setup>
import { onMounted } from "vue"

const Themes = ['light', 'dark']

const setTheme = (color) => {
    //remove previous applied class 
    Themes.forEach((t) => {
        document.documentElement.classList.remove(t)
    })
    document.documentElement.classList.add(color)

}

onMounted(() => {
    let userPreferenceTheme = localStorage.getItem('theme')
    if (!userPreferenceTheme) {
        handleChange()
    } else {
        setTheme(userPreferenceTheme)
    }

})
const media = window.matchMedia('(prefers-color-scheme:dark)')
const handleChange = () => {
    setTheme(media.matches ? 'dark' : 'light')

}
const userPreferenceTheme = localStorage.getItem('theme')
if (!userPreferenceTheme) {
    media.addEventListener('change', handleChange)
}





const switchTheme = () => {
    const currentTheme = document.documentElement.classList.contains("dark") ? "light" : "dark"
    document.documentElement.classList.toggle("dark")
    localStorage.setItem("theme", currentTheme)
}

</script>

<template>
    <div class="min-h-screen bg-background text-forground p-6 transition">
        <ThemeToggle />

        <h1 class="text-4xl font-bold mt-6">
            Scalable Theme System 🚀
        </h1>
        <div class="flex flex-col justify-center items-center mt-10 ">
            <div
                class="w-96 justify-center shadow-sm/20  bg-neutral-50 shadow-black rounded-xl p-2  relative dark:bg-neutral-900  transition">
                <div class="mask-l-from-50% mask-r-from-50%">
                    <div class="h-40 flex justify-center gap-x-6 items-center animate-marquee overflow-hidden ">
                        <span class="rounded-full size-14  text-center text-5xl ">😂</span>
                        <span class="rounded-full size-14  text-center text-5xl ">😁</span>
                        <span class="rounded-full size-14  text-center text-5xl ">😘</span>

                    </div>
                </div>
                <h2 class="font-bold text-2xl font-sans text-neutral-500 dark:text-neutral-100 text-center">Emoji</h2>
                <p class="text-center text-neutral-500 dark:text-neutral-100">Above are the different type of emoji
                    reaction
                </p>
            </div>
            <div class="flex justify-center w-100">
                <button class="rounded-lg cursor-pointer border-2 w-1/2 mt-4 py-2" @click="switchTheme">Switch</button>
            </div>
        </div>
    </div>
</template>
