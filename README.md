1) Какой из двух фрагментов кода не сработает и почему?

Фрагмент 1:

	console.log( doubleNum(10) );

	let doubleNum = (num) => {
		let result = num * 2;
		return result;
	}
Фрагмент 2:

	console.log( doubleNum(10) );

	function doubleNum(num) {
    		let result = num * 2;
		return result;
	}
Ответ: Функции, объявленные как Function Declaration, создаются интерпретатором до выполнения кода. Стрелочные функции, в свою очередь, не обладают таким свойством и поэтому первый фрагмент не сработает

2) Исправьте ошибку в фрагменте коде так, чтобы после компиляции в шаблоне не было лишних тегов:
```
	<template>
		<component-name
			v-for="i of count" 
			:key="i"
			v-if="i < 10" 
		/>
	</template>

	<script>
		export default {
			data() {
				return {
					count: 20;
				};
			},
		};
	</script>  
```
Ответ: Использование дерективы v-if вместе с v-for вызывает ошибку, т.к при их одновременном использовании v-if будет исполняться первым
Первое решение - это написание метода filterCount, который заменяет собой v-if.
Второе - вынести v-for на уровень выше, чтобы не возникало ошибок при их одновременном использовании с v-if. Благодаря фрагменту нет лишних тегов

```
<template>
  <component-name v-for="i of filterCount" :key="i">
  
      {{i + " "}}

  </component-name>
</template>

<script>
export default {
  data() {
    return {
      count: 20
    };
  },
  computed:{
    filterCount(){
      return this.count < 10 ? this.count : 9
    }
  }
};
</script>  
```
или 
```
<template>
  <template v-for="i of count" :key="i">

  
    <component-name v-if="i<10">
    
        {{i + " "}}

    </component-name>
  </template>
</template>

<script>
export default {
  data() {
    return {
      count: 20
    };
  },
};
</script>  
```

3) Есть массив некоторых строительных материалов, каждый элемент массива - объекты с ключами id и количества материала. Напишите функцию, которая будет возвращать oбьект в формате { "id":"count" }
Ответ:

```
resources = [
			{
			   id: 1,
			   count: 13,
   			},
			{
			   id: 2,
			   count: 5,
   			}, 
			{
			   id: 3,
			   count: 24,
   			},
		      {
			   id: 4,
			   count: 101,
   			}, 
			{
			   id: 5,
			   count: 72,
   			}, 
			{
			   id: 6,
			   count: 64,
   			}, 
			{
			   id: 7,
			   count: 305,
   			}, 
			{
			   id: 8,
			   count: 67,
   			}, 
			{
			   id: 9,
			   count: 95,
   			}, 
			{
			   id: 10,
			   count: 21,
   			}, 
			{
			   id: 11,
			   count: 37,
   			},
];
		   
let newObject = {};

let newResources = ()=>{
  for (let item of resources) {
      
      newObject = {
          ...newObject,
          [item.id]: item.count
          
      };
  }
  return newObject
}

console.log(newResources())
```
![image](https://user-images.githubusercontent.com/71041667/193363034-9e70233a-5513-40be-ae4f-99b0bcd2ffaf.png)
