1)Какой из двух фрагментов кода не сработает и почему?

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

Ответ: Использование дерективы v-if вместе с v-for вызывает ошибку, т.к при их одновременном использовании v-if будет исполняться первым
Первое решение - это использование метода filterCount, который заменяет собой v-if.
Второе - вынести v-for на уровень выше, чтобы не возникало ошибок при их одновременном использовании с v-if. Благодаря фрагменту нет лишних тегов


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

или 

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
