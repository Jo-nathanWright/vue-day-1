<template>
  <div class="text-center mt-4 container">
    <div class="row">
      <div class="col-12">
        <img alt="Vue logo" src="./assets/logo.png" />
      </div>
      <div class="col-md-4 mb-4" v-for="t in state.targets" :key="t.id">
        <h3 v-if="t.health > 1">{{ t.role }}</h3>
        <h3 v-else>Unconcious</h3>
        <h1 :class="{ 'text-danger': t.health < 1 }">
          {{ t.name }} - {{ t.health }}
        </h1>
        <button
          :disabled="t.health < 1"
          class="btn btn-primary mr-1"
          @click="attack(1, t)"
        >
          Slap
        </button>
        <button
          :disabled="t.health < 1"
          class="btn btn-warning mr-1"
          @click="attack(2, t)"
        >
          Punch
        </button>
        <button
          :disabled="t.health < 1"
          class="btn btn-danger mr-1"
          @click="attack(3, t)"
        >
          Kick
        </button>
        <button
          v-if="t.health < 1"
          class="btn btn-info"
          @click="t.health = t.maxHealth"
        >
          Defib
        </button>
      </div>
      <h1 v-if="state.allDead">All targets have been eliminated. You are now the owner of Codeworks</h1>
    </div>
  </div>
</template>

<script>
import { reactive } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
export default {
  name: "App",
  setup() {
    //NOTE reactive creates a object where all properties are automatically subscribed to listeners
    const state = reactive({
      targets: [
        {
          id: 1,
          name: "Justin",
          role: "TA",
          health: 80,
          maxHealth: 80,
        },
        {
          id: 2,
          name: "Mark",
          role: "Teacher",
          health: 100,
          maxHealth: 100,
        },
        {
          id: 3,
          name: "Jake",
          role: "Boss",
          health: 120,
          maxHealth: 120,
        },
        {
          id: 4,
          name: "Zack",
          role: "Super Boss",
          health: 200,
          maxHealth: 200,
        },
      ],
      allDead: computed(() =>{
        let dead = true;
        state.targets.forEach(t => {
          if(t.health > 1){
            dead = false;
          }
        })
        return dead
      })
    });

    return {
      attack(val, target) {
        console.log("slap");
        target.health -= val;
        if (target.health < 0) {
          target.health = 0;
        }
      },
      state,
    };
  },
};
</script>

<style scoped>
</style>