# vuex


## State

## Здесь мы определяем структуру данных нашего приложения, а также можем указать значения по умолчанию. Для того, чтобы не быть голословными, давайте определимся, что будем писать приложение для заметок. Соответственно в хранилище нужно положить массив с заметками:

state: {
    notes: []
}

## Actions

## В данной части объявляются методы, которые будут вызывать какие-либо изменения в хранилище. Здесь мы можем сделать запрос к серверу, и после получения ответа вызвать изменение состояния. Actions могут быть вызваны из компонентов с помощью метода dispatch. Мы еще увидим его в действии, а пока просто добавим метод для добавления заметки. Поскольку сервера у нас нет, он будет содержать только следующее:

actions: {
    addNote({commit}, note) {
        commit('ADD_NOTE', note)
    }
}

## commit — это способ вызвать мутацию, изменение состояния. Именование мутаций с помощью заглавных букв не является обязательным, но имеет свой смысл — если в коде встретилось такое название метода, мы можем быть уверены в его предназначении (он изменяет состояние).

## Mutations

## В мутациях изменяется состояние. Здесь не может быть асинхронных вызовов функций, вычислений и.т.д. — только изменение состояния. В нашем примере с добавлением заметки это будет выглядеть примерно так:

mutations: {
    ADD_NOTE(state, note) {
        state.notes.push(note)
    }
}

## Getters

## Для того, чтобы использовать данные, положенные в хранилище, их нужно оттуда достать. Причем часто нам нужны не просто данные, а только часть из них — мы хотим применить к ним какие-то фильтры. Геттеры дают нам такую возможность. В базовом варианте мы можем просто вернуть заметки в том виде, в котором они есть:

getters: {
    notes(state) {
        return state.notes
    }
}

## Modules

## По мере роста приложения хранилище увеличивается и возможность разбить его на части становится все более востребованной. Модули позволяют разделить одно хранилище на несколько хранилищ, но при этом хранить их в виде единого дерева хранилищ.

const moduleA = { state: {}, mutations: {}, actions: {}, getters: {} }
const moduleB = { state: {}, mutations: {}, actions: {}, getters: {} }

const store = new Vuex.Store({
    modules: {
        a: moduleA,
        b: moduleB
    }
})

store.state.a // -> состояние модуля moduleA
store.state.b // -> состояние модуля moduleB 
