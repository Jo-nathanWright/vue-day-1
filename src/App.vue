<template>
<div class="text-center mt-4 container">
  <div class="row">
    <div class="col-12">
      <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <div class='col-md-4 mb-4' v-for="t in state.targets" :key="t.id">
      <h1>{{t.name}} - {{t.health}}</h1>
      <button :disabled="t.health < 1" class="btn btn-primary" @click="attack(1, t)">Slap</button>
      <button :disabled="t.health < 1" class="btn btn-warning" @click="attack(2, t)">Punch</button>
      <button :disabled="t.health < 1" class="btn btn-danger" @click="attack(3, t)">Kick</button>
      <button  v-if="t.health < 1" class="btn btn-info" @click="t.health = t.maxHealth">Defib</button>
    </div>
  </div>
</div>
</template>

<script>
import { reactive } from '@vue/reactivity'
export default {
    name: 'App',
    setup(){
      //NOTE reactive creates a object where all properties are automatically subscribed to listeners
      const state = reactive({
        targets: [{
        id: 1,
        name: 'Mark',
        health: 100,
        maxHealth: 100
      }, {
        id: 2,
        name: 'Jake',
        health: 120,
        maxHealth: 120
      }, {
        id: 3,
        name: 'Justin',
        health: 80,
        maxHealth: 80
      }, {
        id: 4,
        name: 'Zack',
        health: 200,
        maxHealth: 200
      }]
      })
      
      return {
        attack(val, target){
          console.log('slap')
          target.health -= val
          if(target.health < 0){
            target.health = 0
          }
        },
        state
      }
    }
  }
</script>