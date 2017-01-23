### Vuex状态管理

vuex是一个状态管理工具，可以类比为银行，银行的账户是一个state,触发这个state的变化，只能通过银行的业务操作
即state内数据的变化都需要通过访问业务员mutations来进行变化，触发mutations可以直接有银行操作，也可以由用户
访问业务员进行处理，也就是说：
触发state变化：
mutation
action

### mutation 
如下，可以定义一个管理`count`的store,
```javascript
    let store = new Vuex.Store({
        state:{
            count:1
        },
        mutations:{
            increment(state){
                state.count++
            }
        }
    })
```
你不能直接调用该mutation方法，需要采用事件模式进行触发，即：
```javascript
    store.commit('increment)
```
你可以向`store.commit`传入额外的参数，即mutation的*载荷（payload）*:
```javascript
//...
mutations:{
    increment(state,n){
        state.count += n
    }
}
```

也可以采用对象的形式提交，需要包含一个type属性的对象：
```javascript
    store.commit({
        type:'increment',
        amount:10
    })

    //...
    mutations:{
        increment(state,payload){
            state.count += payload.amount
        }
    }
```
mutations用来触发state的变化，是一个同步函数，一个参数是state,第二个参数payload，即：

```javascript
    addToCart(state,{id}){
        state.id = id
    }
```