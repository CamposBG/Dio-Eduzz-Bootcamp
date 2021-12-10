# Aplicando conceitos Rest, Spread Operator e destructing

```js
function sum (a,b){
    return a + b;
}
```

se quisermos que a função acima receba como argumento um numero ilimitado de valores para serem somados, podemos sar o ***Rest Operator*** 

## Rest Operator

> Pega todos os parametros de uma função e transforma em um array

Traz uma lista (de parametros ) e todos os métodos de array para manipular os parametros.

```js
function sum (...args){
    return args.reduce((acc, value) => acc + value, 0)
}

sum(10, 10, 10, 10, 10, 5) // 55
```

O Rest Operator também pode ser tulizado para pegar parametros restantes, 

```js
function fn (a, b ...rest){
    console.log(a, b, rest)
}

fn(10, 3, "car", "cake", 1) // 10 3 "car" "cake" 1
```

> Rest Operator sempre é usado na lista de parametros de uma função

## Spread Operator

> Quebra os itens e passa para algum lugar

Pode ser utilizados em:

- Strings (objeto iteravel)

- Functions call 

- Array Literals

- Obj Literals

#### Arrary Literals

Cria um novo array usando um ourto array pré-existente 

```js
const arr1 = [1,2,3]
const arr2 = [...arr1, 4, 5]
console.log(arr2)
//[1, 2, 3, 4, 5]
```

#### Functions call

Expande qualqer iteravel (array, string, etc) em uma lista de argumentos

```js
const str = "uma string"
function logArgs(...args){ //rest
    console.log(args)
}

logArgs(...str) //spread
// ["u","m","a", " ", "s","t", etc]
```

> em strings especificamente:
> 
> Ela qebra uma string em caracteres e transforma em um array que pode ser passado para outra função



#### Object literals

Copiando propriedades de um objeto para outro. Só pode ser utilizado para se construir novos objetos

```js
const obj1 = {
    name:"harry"
}
const obj2 = {
    ...obj1,
    lastName:"Potter"
}
console.log(obj2)
//{name: 'harry', lastName: 'Potter'}
```

> pode ser usado para clonar objetos "shallow clones" pois não pega objetos aninhados  

## Destructing


