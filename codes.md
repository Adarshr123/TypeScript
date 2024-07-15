CHAPTER - 1 START HERE
let username = "Shruti"
console.log(username);

let a : number = 12
let b : number = 6
let c : number = 2
console.log(a/b)
console.log(c*b)


CHAPTER - 2 BASIC TYPES
// let myName = 'Adarsh' // Implicit
let myName: string = 'Adarsh' // Explicit
let meaningOfLife: number;
let isLoading: boolean;
let album: any;

myName = 'Shruti'
meaningOfLife = 42
isLoading = false
album = true

const sum = (a:number, b:number) => {
    return a + b;
}

let postId: string | number;
let isActive: number | boolean;

let re: RegExp = /\w+/g


CHAPTER - 3 ARRAYS & OBJECTS
/* Arrays and objects */

let stringArr = ['one', 'hey', 'Adarsh']

let guitars = ['Strat', 'Les Paul', 5150]

let mixedData = ['EVH', 1984, true]

stringArr[0] = 'John'
stringArr.push('hey')

guitars[0] = 1984
guitars.unshift('Jim')

let test = []
let bands: string[] = []
bands.push('Van Halen')

// Tuple
let myTuple: [string, number, boolean] = ['Adarsh', 42, true]
let mixed = ['John', 1, false]

myTuple[1] = 32

// Objects
let myObject: object
myObject = []
console.log(typeof myObject)
myObject = bands
myObject = {}

const exampleObj = {
    prop1: 'Dave',
    prop2: true,
}

exampleObj.prop1 = 'John'

// type Guitarist = {
//     name: string,
//     active?: boolean,
//     albums: (string | number)[]
// }

interface Guitarist {
    name?: string,
    active: boolean,
    albums: (string | number)[]
}

let evh: Guitarist = {
    name: 'Eddie',
    active: false,
    albums: [1984, 5150, 'OU812']
}

let jp: Guitarist = {
    active: true,
    albums: ['I', 'II', 'IV']
}

const greetGuitarist = (guitarist: Guitarist) => {
    // narrowing
    if(guitarist.name) {
        return `Hello ${guitarist.name.toUpperCase()}!`
    }
    return 'Hello!'
}

console.log(greetGuitarist(jp))

// Enums
// Unlike most Typescript features, Enums are not a type-level addition to JavaScript but something added to the language and runtime.

enum Grade {
    U = 1,
    D,
    C,
    B,
    A,
}

console.log(Grade.U)


CHAPTER - 4 FUNCTIONS

/* Functions */

// Type Aliases
type stringOrNumber = string | number

type stringOrNumberArray = (string | number)[]

type Guitarist = {
    name?: string,
    active: boolean,
    albums: (string | number)[]
}

type UserId = stringOrNumber

// interface PostId = stringOrNumber - won't work

// Literal types
let myName: 'Dave'

let userName: 'Dave' | 'John' | 'Amy'
userName = 'Amy'

// functions
const add = (a: number, b: number): number => {
    return a + b;
}

const logMsg = (message: any): void => {
    console.log(message)
}

logMsg('Hello')
logMsg(add(2,3))
// logMsg(add('a', 3))

let substract = function(c:number, d: number): number {
    return c - d
}

type mathFunction = (a: number, b: number) => number

// interface mathFunction { 
//     (a: number, b: number) : number 
// }

let multiply: mathFunction = function(c, d) {
    return c * d
}

logMsg(multiply(2,2))

// optional parameters
const addAll = (a: number, b: number, c?:number) : number => {
    if(typeof c !== 'undefined') {
        return a + b + c
    }
    return a + b
}

// default param value
const sumAll = (a: number = 10, b: number, c:number = 2) : number => {
    return a + b + c
}

logMsg(addAll(2,3,2))
logMsg(addAll(2,3))
logMsg(sumAll(2,3))
logMsg(sumAll(undefined,3))

// Rest Parameters
const total = (...nums: number[]): number => {
    return nums.reduce((prev, curr) => prev + curr)
}

logMsg(total(1,2,3,4))

const createError = (errMsg: string): never => {
    throw new Error(errMsg)
}

const infinite = () => {
    let i: number = 1;
    while(true) {
        i++
        if(i > 100) break
    }
}

// custom type guard
const isNumber = (value: any): boolean => {
    return typeof value === 'number'
    ? true : false
}

// use of the never type
const numberOrString = (value: number | string): string => {
    if(typeof value === 'string') return 'string'
    if(typeof value === 'number') return 'number'
    return createError('This should never happen!')
}