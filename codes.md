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


CHAPTER - 5 ASSERTION

type One = string
type Two = string | number
type Three = 'hello'

// convert to more or less specific
let a: One = 'hello'
let b = a as Two // less specific
let c = a as Three // more specific

let d = <One>'world'
let e = <string | number>'world'

const addOrConcat = (a: number, b: number, c: 'add' | 'concat'): number | string => {
    if(c === 'add') return a + b
    return '' + a + b
}

let myVal: string = addOrConcat(2,2,'concat') as string

// Be careful! TS sees no problem - but a string is returned
let nextVal: number = addOrConcat(2,2,'concat') as number

// 10 as string
(10 as unknown) as string

// The DOM (Document Object Model)
const img = document.querySelector('img')!
const myImg = document.getElementById('#img') as HTMLImageElement
const nextImg = <HTMLImageElement>document.getElementById('#img')

img.src
myImg.src



// Original JS code
// const year = document.getElementById("year")
// const thisYear = new Date().getFullYear()
// year.setAttribute("datetime", thisYear)
// year.textContent = thisYear

// 1st variation:
// let year: HTMLElement | null
// year = document.getElementById("year")
// let thisYear: string
// thisYear = new Date().getFullYear().toString()
// if(year) {
//     year.setAttribute("datetime", thisYear)
//     year.textContent = thisYear
// }

// 2nd variation:
const year = document.getElementById("year") as HTMLSpanElement
const thisYear = new Date().getFullYear().toString()
year.setAttribute("datetime", thisYear)
year.textContent = thisYear



// CHAPTER - 6 CLASSES

class Coder {
    secondLang!: string
    constructor(
        public readonly name: string, 
        public music: string, 
        private age: number, 
        protected lang: string =  'Typescript'
    ) {
        this.name = name
        this.music = music
        this.age = age
        this.lang = lang
    }

    public getAge() {
        return `Hello, I'm ${this.age}`
    }
}

const Dave = new Coder('Dave', 'Rock', 42)
console.log(Dave.getAge())
// console.log(Dave.age)
// console.log(Dave.lang)

class WebDev extends Coder {
    constructor(
        public computer: string,
        name: string,
        music: string,
        age: number
    ) {
        super(name, music, age)
        this.computer = computer
    }

    public getLang() {
        return `I write ${this.lang}`
    }
}

const Sara = new WebDev('Mac', 'Sara', 'Lofi', 25)
console.log(Sara.getLang())
// console.log(Sara.age)
// console.log(Sara.lang)

interface Musician {
    name: string,
    instrument: string,
    play(action: string): string
}

class Guitarist implements Musician {
    name: string
    instrument: string

    constructor(name: string, instrument: string) {
        this.name = name
        this.instrument = instrument
    }

    play(action: string) {
        return `${this.name} ${action} the ${this.instrument}`
    }
}

const Page = new Guitarist('Jimmy', 'guitar')
console.log(Page.play('strums'))


class Peeps {
    private static count: number = 0

    static getCount(): number {
        return Peeps.count
    }

    public id: number
    constructor(public name: string) {
        this.name = name
        this.id = ++Peeps.count
    }
}

const John = new Peeps('John')
const Steve = new Peeps('Steve')
const Amy = new Peeps('Amy')

console.log(Peeps.getCount())

console.log(Amy.id)
console.log(Steve.id)
console.log(John.id)


class Bands {
    private dataState: string[]

    constructor() {
        this.dataState = []
    }

    public get data(): string[] {
        return this.dataState
    }

    public set data(value: string[]) {
        if(Array.isArray(value) && value.every(el => typeof el === 'string')) {
            this.dataState = value
            return
        } else throw new Error('Param is not an array of strings')
    }
}

const MyBands = new Bands()
MyBands.data = ['Neil Young', 'Led Zep']
console.log(MyBands.data)
MyBands.data = [...MyBands.data, 'ZZ Top']
console.log(MyBands.data)


CHAPTER 7 - Index Signature & keyof Assertion

// interface TransactionObj {
//     readonly [index: string]: number
// }

interface TransactionObj {
    readonly [index: string]: number
    Pizza: number,
    Books: number,
    Job: number
}

const todaysTransactions: TransactionObj = {
    Pizza: -10,
    Books: -5,
    Job: 50,
    Adarsh: 69
}

console.log(todaysTransactions.Pizza)
console.log(todaysTransactions['Pizza'])

let prop: string = 'Pizza'
console.log(todaysTransactions[prop])

const todaysNet = (transactions: TransactionObj): number => {
    let total = 0
    for(const transaction in transactions) {
        total += transactions[transaction]
    }
    return total
}

console.log(todaysNet(todaysTransactions))
// todaysTransactions.Pizza = 40

console.log(todaysTransactions['Adarsh'])


interface Student {
    // [key: string]: string | number | number[] | undefined
    name: string,
    GPA: number,
    classes?: number[]
}

const student: Student = {
    name: "Adarsh",
    GPA: 7.9,
    classes: [100, 200]
}

// console.log(student.test)

for(const key in student) {
    console.log(`${key}: ${student[key as keyof Student]}`)
}

Object.keys(student).map(key => {
    console.log(student[key as keyof typeof student])
})

const logStudentKey = (student: Student, key: keyof Student): void => {
    console.log(`Student ${key}: ${student[key]}`)
}

logStudentKey(student, 'GPA')
logStudentKey(student, 'classes')



// interface Incomes {
//     [key: string]: number
// }

type Streams = 'salary' | 'bonus' | 'sidehustle'

type Incomes = Record<Streams, number | string>

const monthlyIncomes: Incomes = {
    salary: 500,
    bonus: 100,
    sidehustle: 250
}

for (const revenue in monthlyIncomes) { 
    console.log(monthlyIncomes[revenue as keyof Incomes])
}


// Index Signature & keyof Assertion

// interface TransactionObj {
//     readonly [index: string]: number
// }

interface TransactionObj {
    readonly [index: string]: number
    Pizza: number,
    Books: number,
    Job: number
}

const todaysTransactions: TransactionObj = {
    Pizza: -10,
    Books: -5,
    Job: 50,
    Adarsh: 69
}

console.log(todaysTransactions.Pizza)
console.log(todaysTransactions['Pizza'])

let prop: string = 'Pizza'
console.log(todaysTransactions[prop])

const todaysNet = (transactions: TransactionObj): number => {
    let total = 0
    for(const transaction in transactions) {
        total += transactions[transaction]
    }
    return total
}

console.log(todaysNet(todaysTransactions))
// todaysTransactions.Pizza = 40

console.log(todaysTransactions['Adarsh'])


interface Student {
    // [key: string]: string | number | number[] | undefined
    name: string,
    GPA: number,
    classes?: number[]
}

const student: Student = {
    name: "Adarsh",
    GPA: 7.9,
    classes: [100, 200]
}

// console.log(student.test)

for(const key in student) {
    console.log(`${key}: ${student[key as keyof Student]}`)
}

Object.keys(student).map(key => {
    console.log(student[key as keyof typeof student])
})

const logStudentKey = (student: Student, key: keyof Student): void => {
    console.log(`Student ${key}: ${student[key]}`)
}

logStudentKey(student, 'GPA')
logStudentKey(student, 'classes')



// interface Incomes {
//     [key: string]: number
// }

type Streams = 'salary' | 'bonus' | 'sidehustle'

type Incomes = Record<Streams, number | string>

const monthlyIncomes: Incomes = {
    salary: 500,
    bonus: 100,
    sidehustle: 250
}

for (const revenue in monthlyIncomes) { 
    console.log(monthlyIncomes[revenue as keyof Incomes])
}


// CHAPTER - 8 Generics
const echo = <T>(arg: T): T => arg

const isObj = <T>(arg: T): boolean => {
    return (typeof arg === 'object' && !Array.isArray(arg) && arg !== null)
}

console.log(isObj(true))
console.log(isObj('John'))
console.log(isObj([1, 2, 3]))
console.log(isObj({name : 'John'}))
console.log(isObj(null))

const isTrue = <T>(arg: T): {arg: T, is: boolean} => {
    if(Array.isArray(arg) && !arg.length) {
        return {arg, is: false}
    }
    if(isObj(arg) && !Object.keys(arg as keyof T). length) {
        return {arg, is: false}
    }
    return {arg, is: !!arg }
}

console.log(isTrue(false))
console.log(isTrue(0))
console.log(isTrue(true))
console.log(isTrue(1))
console.log(isTrue('Adarsh'))
console.log(isTrue(''))
console.log(isTrue(null))
console.log(isTrue(undefined))
console.log(isTrue({}))
console.log(isTrue({name: 'Adarsh' }))
console.log(isTrue([]))
console.log(isTrue([1, 2, 3]))
console.log(isTrue(NaN))
console.log(isTrue(-0))

interface BoolCheck<T> {
    value: T,
    is: boolean
}

const checkBoolValue = <T>(arg: T): BoolCheck<T> => {
    if(Array.isArray(arg) && !arg.length) {
        return { value: arg, is: false}
    }
    if(isObj(arg) && !Object.keys(arg as keyof T). length) {
        return {value: arg, is: false}
    }
    return {value: arg, is: !!arg }
}

interface HasID {
    id: number
}

const processUser = <T extends HasID>(user: T): T => {
    // process the use with logic
    return user
}

console.log(processUser({id: 1, name: 'Adarsh'}))
// console.log(processUser({name: 'Adarsh'}))

const getUsersProperty = <T extends HasID, K extends keyof T>(users: T[], key: K): T[K][] => {
    return users.map(user => user[key])
}

const usersArray = [
    {
        "id": 1,
        "name": "Leanne Graham",
        "username": "Bret",
        "email": "Sincere@april.biz",
        "address": {
            "street": "Kulas Light",
            "suite": "Apt. 556",
            "city": "Gwenborough",
            "zipcode": "92998-3874",
            "geo": {
                "lat": "-37.3159",
                "lng": "81.1496"
            }
        },
        "phone": "1-770-736-8031 x56442",
        "website": "hildegard.org",
        "company": {
            "name": "Romaguera-Crona",
            "catchPhrase": "Multi-layered client-server neural-net",
            "bs": "harness real-time e-markets"
        }
    },
    {
        "id": 2,
        "name": "Ervin Howell",
        "username": "Antonette",
        "email": "Shanna@melissa.tv",
        "address": {
            "street": "Victor Plains",
            "suite": "Suite 879",
            "city": "Wisokyburgh",
            "zipcode": "90566-7771",
            "geo": {
                "lat": "-43.9509",
                "lng": "-34.4618"
            }
        },
        "phone": "010-692-6593 x09125",
        "website": "anastasia.net",
        "company": {
            "name": "Deckow-Crist",
            "catchPhrase": "Proactive didactic contingency",
            "bs": "synergize scalable supply-chains"
        }
    },
]

console.log(getUsersProperty(usersArray, "website"))
console.log(getUsersProperty(usersArray, "username"))


class StateObject<T> {
    private data: T
    constructor(value: T) {
        this.data = value
    }

    get state(): T {
        return this.data
    }

    set state(value: T) {
        this.data = value
    } 
}

const store = new StateObject("John")
console.log(store.state)
store.state = "Adarsh"
// store.store = 12

const myState = new StateObject<(string | number | boolean)[]>([15])
myState.state = (['Adarsh', 23, true])
console.log(myState.state)

