<template>
    <div class="calc-height flex items-center justify-center flex-col text-center px-4">
        <div class="relative z-10 flex items-center text-center justify-center flex-col">
            <h2 class="text-2xl sm:text-4xl">Hi, My name is <span class="text-blue-400">Daniel</span></h2>
            <Transition name="text">
                <p class="text-xl sm:text-2xl mt-6 block w-fit" :key="text">{{ text }}</p>
            </Transition>
            <button class="mt-6 animation-right">
                <NuxtLink to="/skills">
                    <svg xmlns="http://www.w3.org/2000/svg" class="fill-blue-400 bg-blue-400/5 rounded-full h-8 w-8"
                        viewBox="0 0 16 16">
                        <path fill-rule="evenodd"
                            d="M4 8a.5.5 0 0 1 .5-.5h5.793L8.146 5.354a.5.5 0 1 1 .708-.708l3 3a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708-.708L10.293 8.5H4.5A.5.5 0 0 1 4 8" />
                    </svg>
                </NuxtLink>
            </button>
            <div class="mt-5">
				<ul class="text-center flex gap-3 flex-wrap justify-center">
					<li>
						<a href="//imdanieln.t.me" target="_blank"
							class="px-3 py-1 border-2 border-double border-blue-600 uppercase transition-colors hover:bg-blue-600">
							Telegram
						</a>
					</li>
					<li>
						<a href="#" @click="copytoclipboard('danialnasronline@gmail.com')"
							class="px-3 py-1 border-2 border-double border-blue-600 uppercase transition-colors hover:bg-blue-600">
							Email
						</a>
					</li>
					<li>
						<a href="//github.com/imdanieldev" target="_blank"
							class="px-3 py-1 border-2 border-double border-blue-600 uppercase transition-colors hover:bg-blue-600">
							Github
						</a>
					</li>
				</ul>
			</div>
            <Transition name="alert">
		<div v-if="alertshow" class="z-50 fixed bottom-5 text-base right-1/2 translate-x-1/2 bg-black/20 backdrop-blur-lg px-4 py-2 border-2 border-solid border-blue-600 text-center">
			{{ alerttext }}
		</div>
		</Transition>
        </div>
        <div class="opacity-10 absolute w-5 h-5">
            <TresCanvas window-size>
                <TresPerspectiveCamera :position="[2.5, 2.5, 2.5]" />
                <OrbitControls />
                <TresMesh :position="[0, 0, 0]" cast-shadow>
                    <TresBoxGeometry :args="[2, 2, 2]" />
                    <TresMeshToonMaterial color="#ffffff" />
                </TresMesh>
                <TresDirectionalLight :position="[0, 10, 5]" :intensity="2.0" cast-shadow />
            </TresCanvas>
        </div>
    </div>
</template>
<script setup>
import { TresCanvas } from '@tresjs/core';
import { OrbitControls } from '@tresjs/cientos';
const d = new Date();
const year = d.getFullYear();
const Age = ref(year - 2008);
const texts = ref(["I'm Web Developer", "I'm Student", "I'm "+ Age.value +"yo", "I'm Frontend Developer", "I'm Backend Developer", "I know wordpress", "I know Linux", "I Love Programming"]);
const text = ref(texts.value[0]);
const i = ref(1);
function changetext() {
    if (i.value == texts.value.length) {
        i.value = 0;
        text.value = texts.value[i.value];
    } else {
        text.value = texts.value[i.value];
        i.value++;
    }
}
const alertshow = ref(false);
const alerttext = ref("nothing");
function myalert(yourtext){
	alertshow.value = true;
	alerttext.value = yourtext
	setTimeout(()=>{
		alertshow.value = false;
	},4000);
}
function copytoclipboard(yourtext){
	navigator.clipboard.writeText(yourtext);
	myalert("The email was saved to the clipboard.")
}
onMounted(() => {
    setInterval(() => {
        changetext()
    }, 2500);
});
useHead({
    title: 'Daniel Web Dev',
});
</script>
<style>
.alert-enter-active,
.alert-leave-active {
	transition: 0.2s ease;
}

.alert-enter-from,
.alert-leave-to {
	bottom: calc(-1.2rem - 1rem - 2px - 2.5rem);
}
.text-enter-active,
.text-leave-active {
    transition: all 0.4s cubic-bezier(0.19, 1, 0.22, 1);
}

.text-enter-from {
    position: absolute;
    opacity: 0;
    transform: translateY(-30px);
}

.text-leave-to {
    position: absolute;
    opacity: 0;
    transform: translateY(30px);
}

.animation-right {
    animation: bounce 1s infinite;
}

@keyframes bounce {

    0%,
    100% {
        transform: translateX(-25%);
        animation-timing-function: cubic-bezier(0.8, 0, 1, 1);
    }

    50% {
        transform: translateX(0);
        animation-timing-function: cubic-bezier(0, 0, 0.2, 1);
    }
}
</style>
