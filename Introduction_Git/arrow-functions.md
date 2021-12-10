# Funções

## Arrow functions

## Observações sobre arrow functions

- Não pode ser usada em funcções construtoras :

```js
function car (){
    this.foo = 'bar'
}
new car()
```

- Hoisting não funciona com arrow functions. Eu preciso definiar e criar a função antes de invocar ou rodar ela

- ***This*** em arrow functions:
  
  - A arroe function possui um contexto igual ao condigo que envolve ele, ao se obervar as chaves ao redor da arrow function  é possivel saber a o que This está refenciando.
    
    ```js
    var obj = {
        showContext: function showContext(){ //chave incio
            // this = obj
            setTimeout( () => {
                this.log("after 1000ms")
            }, 1000);
        }, //chave fim
        log: function lg(value) {
            console.log(value)
        }
    };
    
    obj.showContext();
    ```
  
  - **Sem** uma arrow function, this no codigo acima aponta para o windown já que as funções tem o contexto de invocação e o método setTimeout é um método de contexto globla no caso *Window*

## Default Functions Arguments

```js
function multiply (a, b = a){
    return a * b,
    method1 (parameter1, paramete2) {
        // do something 
    }
}
```

No caso acima definimos um valor padrão para b, que caso esse argumento nao seja fornececido ao chamar a função ele vai receber o valor de a. 

Nesses casos a ordem importa,  antes do argumento receber algum valor, ele deve ser criado, por ex. ``function mltiply (b = a, a){`` não iria funcionar pois ***a*** é declarada depois de atribuir o valor a ***b***.

### Lazy evaluation

```js
function randomNumber(){
    return Math.random()*10;
}
function multiply(a, b = randomNumber()){
    retutn a * b;
}

multiply(5)
    // 5 * randNum
```

Sempre que você deixa de passar um argumento para uma função ela vai incovar a função determinada.   

> Isso é bom para gerar IDs randomicos ou disparar erros se alguem esquecer de passar algum parametro. Ou em qualquer situação onde uma função possa gerar um valor.



## Enhended Object literals

### Modo Clássico de se escrever objetos:

```js
const obj = {
    key: 'value',
};
```

### Também é possivel referenciar um valor de uma propriedade:

```js
const prop1 = "value"
const obj = {
    ey: prop1,
};
```

Se o a key e a value da Propr tem o mesmo valor posso simplesmente usar:

```js
const prop1 = "value"
const obj = {
 prop1, // prop1: prop1
};
```

O mesmo se aplica a métodos. 

### Propriedades computadas

```js
const propName = 'teste'

const obj = {
    [propName + '-concat'] : "prop value"
}

console.log(obj)
    // obj{ teste-concat: "prop value"}
```


