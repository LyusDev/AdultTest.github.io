<template>
  <div class="mx-5 shadow-2xl">
    <div class="flex bg-black">
      <h1 class="text-5xl text-white uppercase font-bold w-8/12 pl-5">What is your adulting score?</h1>
      <input
        class="bg-yellow-300 ml-5 w-4/12 shadow appearance-none border border-black rounded py-2 px-3 text-gray-900 focus:outline-none focus:shadow-outline"
        id="username"
        type="text"
        placeholder="Enter your name here."
        v-model="yourname"
      />
    </div>
    <div class="flex">
      <div class="px-5 w-1/2 bg-yellow-300">
        <div class="flex justify-between items-center" v-for="task in data.tasks" :key="task.id">
          <div class="flex">
            <div class="text-xl text-black font-bold mr-2">{{task.id}}).</div>
            <div class="text-xl text-black font-bold mr-2">{{task.pts}}pts</div>
            <div class="text-xl text-black ml-2">{{task.desc}}</div>
          </div>
          <input
            type="checkbox"
            id="checkbox"
            v-model="selected"
            v-bind:value="task.pts"
            :key="task.id"
          />
        </div>
        <div class="flex mb-5 mt-3">
          <button
            class="w-full bg-black text-white text-xl p-2 rounded-lg border-yellow-400 border-2 hover:bg-yellow-600"
            v-on:click="ishidden = !ishidden"
          >Submit</button>
          <a href="/">
            <button
              type="reset"
              class="w-full bg-black text-white text-xl p-2 rounded-lg border-yellow-400 border-2 hover:bg-yellow-600"
            >Reset</button>
          </a>
        </div>
      </div>
      <div class="px-5 p-5 w-1/2 bg-yellow-400">
        <div class="bg-white" v-for="result in data.countpts" :key="result.age">
          <div class="mb-2 flex items-center">
            <div class="text-xl text-white font-bold bg-black p-2 mr-2 rounded-lg"  v-bind:class="hResult(sum[1])" hidden:false>{{result.pts}}</div>
            <div class="text-xl text-black">{{result.desc}}</div>
          </div>
        </div>
        <div class="text-2xl text-white bg-black uppercase font-bold mb-5 p-2">Result</div>
        <div
          class="text-2xl text-black font-bold p-2 mr-2 rounded-lg w-auto uppercase"
        >Your name is: {{ yourname}} ♥</div>
        <div v-if="ishidden == false">
          <div class="text-5xl text-black font-bold p-2 mr-2 rounded-lg w-auto">Congratulation!!</div>
          <div
            class="text-2xl text-black font-bold p-2 mr-2 rounded-lg w-auto"
          >Your Score: {{ sum[1] }}</div>
          <div
            class="text-2xl text-black font-bold p-2 mr-2 rounded-lg w-auto"
          >Ikaw ay: {{ sum[0] }} !!</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import data from "../data.json";
export default {
  data() {
    return {
      data: data,
      selected: [],
      ishidden: true,
      show: true,
      yourname: null,
    };
  },
  computed: {
    hResult(value){

        if (value >= 5 && value <= 50) {
        return 'text-red-900';
    }

    },
    sum() {
      var sem = this.selected.reduce(function (a, b) {
        return parseInt(a) + parseInt(b);
      }, 0);

      if (sem >= 5 && sem <= 50) {
        return [this.data.countpts[1].age, sem];
      } else if (sem >= 50 && sem <= 99) {
        return [this.data.countpts[2].age, sem];
      } else if (sem >= 100 && sem <= 149) {
        return [this.data.countpts[3].age, sem];
      } else if (sem >= 150 && sem > 200) {
        return [this.data.countpts[4].age, sem];
      } else {
        return ["New born baby", sem];
      }
    }
  }
};
</script>