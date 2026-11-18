<script setup>
import { ref, computed } from 'vue'

const people = ref([
  { name: 'Jan', age: 12 },
  { name: 'Piet', age: 20 }
])

const newName = ref('')
const newAge = ref(null)


const children = computed(() => {
  return people.value.filter((p) => p.age < 18)
})

const Adults = computed (() => {
  return people.value.filter((p) => p.age >= 18)
}) 

const totalepeople = computed (() => {
return people.value.length
})

const numberOfChildren = computed (() => {
return children.value.length
})

function addPerson() {
 
  if (!newName.value || newAge.value === null || newAge.value === '') return

 
  people.value.push({
    name: newName.value,
    age: newAge.value
  })

  
  newName.value = ''
  newAge.value = null
}
</script>

<template>
  <div>
  
    <input v-model="newName" placeholder="Naam" />
    <input v-model.number="newAge" type="number" placeholder="Leeftijd" />
    

    <button @click="addPerson">Toevoegen</button>

   
    <h3>Alle personen:</h3>
    <ul>
      <li v-for="(person, index) in people" :key="index">
        {{ person.name }} ({{ person.age }} jaar)
      </li>
    </ul>

    <h3>Kinderen (jonger dan 18):</h3>
    <ul>
      <li v-for="(child, index) in children" :key="index">
        {{ child.name }} ({{ child.age }} jaar)
      </li>
    </ul>

    <h3>volwassenen</h3>
      <ul>
<li v-for="(adult, index) in Adults" key="index1">
{{adult.name}} ({{adult.age}} jaar)
</li>
    </ul>

    <h3>totaal aantal mensen {{totalepeople}}</h3>
    
    <h3>totaal aantal kinderen {{numberOfChildren}}</h3>
  </div>
</template>
