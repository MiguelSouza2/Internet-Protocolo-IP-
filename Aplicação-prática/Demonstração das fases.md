# <font style="color: #FF5582A6;">FASE VERMELHA</font> <mark style="background: #FF5582A6;">[ Red phase ]</mark>
## calc.test.js
```jest
// deve falhar, pois não existe o indexedDB.soma ainda. (FASE VERMELHA)

  

test("Retorna valor", () => {

    let res = indexedDB.soma(5,5);

    expect(res).toEqual(10);

})
```

## index.js
```js
// ainda está vazio
```

## Terminal resposta
> Deve retornar erro pois a função index.soma ainda não existe ainda no index.js
> 
```powershell
PS C:\qts\tdd-calc> npx jest  
 FAIL  ./calc.test.js
  × Retorna valor (2 ms)
                                                                                                                                                                                
  ● Retorna valor                                                                                                                                                               
                                                                                                                                                                                
    ReferenceError: indexedDB is not defined

      2 |
      3 | test("Retorna valor", () => {
    > 4 |     let res = indexedDB.soma(5,5);
        |               ^
      5 |     expect(res).toEqual(10);
      6 | })

      at Object.indexedDB (calc.test.js:4:15)

Test Suites: 1 failed, 1 total                                                                                                                                                  
Tests:       1 failed, 1 total                                                                                                                                                  
Snapshots:   0 total
Time:        0.542 s
Ran all test suites.
```

---

# <font style="color: #BBFABBA6;">FASE VERDE</font> <mark style="background: #BBFABBA6;">[ Green Phase ]</mark>
## calc.test.js
```jest
// deve funcionar agora. (FASE VERDE)

const index = require('./index');

  

test("Retorna valor", () => {

    let res = index.soma(5,5);

    expect(res).toEqual(10);

})
```

## index.js
```js
module.exports = {

    soma: function(a, b) {

        return a + b;

    }

}
```

## Terminal
> Incluindo a função de soma no index e exportando no código de teste, deve funcionar.
```powershell
PS C:\qts\tdd-calc> npx jest
 PASS  ./calc.test.js
  √ Retorna valor (3 ms)

Test Suites: 1 passed, 1 total                                                                                                                                                  
Tests:       1 passed, 1 total                                                                                                                                                  
Snapshots:   0 total
Time:        0.637 s, estimated 2 s
Ran all test suites.
```

---

# <font style="color: #ADCCFFA6;">FASE REFACTOR</font> <mark style="background: #ADCCFFA6;">[ Refactor ]</mark>
## calc.test.js
```jest
// deve funcionar agora. (FASE VERDE)

const index = require('./index');

  

test("Retorna valor", () => {

    let res = index.soma(5,5);

    expect(res).toEqual(10);

})
```

## index.js
```js
// fase Refactor
// retira a palavra function e utiliza arrow function

module.exports = {

    soma:(n1,n2) => {

        return n1 + n2;

    }

}
```

## Terminal
> Note que dessa vez foi ganhado 0.005s em comparação com o resultado anterior
```powershell
PS C:\qts\tdd-calc> npx jest
 PASS  ./calc.test.js
  √ Retorna valor (5 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.632 s, estimated 1 s
Ran all test suites.
```
