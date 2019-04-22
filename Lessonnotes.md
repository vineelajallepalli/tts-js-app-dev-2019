# ES6 notes
  

###  templata literal are enclosed by back ticks(`)
```javascript
console.log(`Hello! Im a string
continues on this line`);
```
### strings can be displayed in multilines using (\n)
```javascript
console.log("string text 1\n"
+ "string text 2");
```
### concatenation can done with ${} instead of + operator
```javascript
const name="jimmy"
const day="wednesday"
const instructor = {
    name: "chris",
    lesson:"ES6",
    greet: function(){
        return ` ${this.name} teaches ${this.lesson} today`
    }
}

console.log("Hello"+ name + "I hope you have a great day on"+ day);

console.log(`Hello ${name} I hope ${day}goes well!`);

console.log(` ${instructor.name} teaches ${instructor.lesson} today`);

console.log(instructor.greet());
```
### Here let is limited to the if block only
```javascript
function foo(){

    let x= true;
    if (x){
         let usingVar="im using let";
          console.log(usingVar);
 }

 foo();//undefined
 ```
```javascript
 const instructors = ["Jimmy","Chris"];
 instructors = ["Jim","Chris"];//const cant be renamed
```
```javascript
instructors.push("Jack","Jill");//but const can be modified

console.log(instructors);

//const also accepts uppercase
```
## ES5
```javascript
function hello(name){
    name = name || 'Mystery Person';
    console.log("Hello"+ name + "!")
}
hello("Bobby");
hello();
```
## ES6
```javascript


function hello(name='Mystery Person'){
    console.log(`Hello ${name} is it me you are looking for`)
}

hello("Bobby");
hello();
```
## ES5
```javascript
const teacher = {
    name: "Jimm",
    speak=function(){
        // bind afunction to a specific content
        let boundFunction=function(){
            console.log("later my name is"+this.name);
        }.bind(this);
        // boundfunction will always run in bound context
        setTimeout(boundFunction,1000);
    }
// };
teacher.speak();
```
## ES6 using arrow funcitons
```javascript

const teacher = {
    name: "Jimm",
    speak(){
        // bind afunction to a specific content
        let boundFunction=()=>{
            console.log("later my name is"+this.name);
        };
        // boundfunction will always run in bound context
        setTimeout(boundFunction,1000);
    }
};
teacher.speak();
// lexical binding - they bind to cope where defined not where they are used
```
## arrow functions implicitly return
```javascript
let students=[
    { name: 'Ashley'},
    {name: 'suji'},
    {name:'vandana'},
    {name: 'Deepti'}
];
//let names = students.map((student)=> student.name);
// same as
let names=students.map((student)=>{
    return student.name;
})
console.log(names);
```
## ES5
```javascript
function add(){
    console.log("arguments object:",arguments);
    var numbers =Array.prototype.slice.call(arguments);
    var sum=0;
    numbers.forEach(function(number){
        sum+=number;
    });
    return sum;
}
console.log(add(1,2,3,4,5,6,7,8));
// arguments object: {"0":1,"1":2,"2":3,"3":4,"4":5,"5":6,"6":7,"7":8}
// 36
```
## ES6
```javascript
let add=(...numbers)=> {
    console.log("rest parameters", numbers);
    let sum=0;
    numbers.forEach(function(number){
            sum +=number;
            });
            return sum;
       }
         console.log(add(1,2,3,4,5,6,7,8));
         // rest parameters: [1,2,3,4,5,6,7,8]
        // 36
```        
        
## Rest example all on same line
```javascript
        let add=(...numbers)=>numbers.reduce((sum,number)=>sum+=number,0);
             console.log(add(1,2,3,4,5,6,7,8));
```
### combine rest parameters with multiple arguments
```javascript
             function addStuff(x,y,...z){
                 return(x+y)*z.length
             }
             console.log(addStuff(1,2,"hello","world",true,99));
            //12
```

## spread operator
```javascript
             let random=["Hello","World",true,99]
             let newArray=[1,2,...random,3]

             console.log(newArray);
             [1,2,"Hello","World",true,99,3]
```
```javascript
             let spreadEx = (item) => {
                 let spreadArray = [...item]
                 console.log(spreadArray);
                 return spreadArray
             }

             spreadEx("Hello World")
             [ 'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd' ]
```
```javascript
            let restEx = (...z) => {
                console.log(z)
                return z
            }

            restEx("hello","world")
            //[ 'hello', 'world' ]
```
### Destructuring
## ES5
```javascript

            var students=["A","B","C"];
            var x = students[0];
            var y = students[1];
            var z = students[2];
            console.log(x,y,z);
            //A B C
```
## ES6
```javascript
            let students=["Julian","AJ","Matt"];
             let [x,y,z]=students
             //let[x, ,z]=students
             //let [x, ...rest]=students;
             console.log(x, rest);
             //Julian["AJ","Matt"]
```
## Destructuring with functions
```javascript
             let completedHomework = () => {
                 return ["Julian","AJ","Matt"];
             }
             let [x,y,z]=completedHomework();
             console.log(x,y,z);
```
## Also works with objects
```javascript
             
             let instructor = {
                 name: "Jimmy",
                 email: "no@no.com"
             }
             let { name: x, email: y } = instructor;
             console.log(x);
             //Jimmy
```
```javascript
             let instructor = {
                name: "Jimmy",
                email: "no@no.com"
             }
             function something({name,email,phone=123}) {
                console.log(name,email,phone) ;
             }
             something(instructor);
```
## Classes -ES5
```javascript
            function Person (name, job){
                this.name = name;
                this.job = job;
            }
            Person.prototype.getName = function getName(){
                return this.name;
            }
            
            var goodGuy = new Person ("Aang","Airbender");
            console.log(goodGuy.getName());

            
            function Person (name, job){
                this.name = name;
                this.job = job;
            }
            Person.prototype.getJob = function getJob(){
                return this.job;
            }
            
            var goodJob= new Person ("Aang","Airbender");
            console.log(goodJob.getJob());
```    
## ES6
```javascript        

            class Person{
                constructor(name,job){
                    this.name = name;
                    this.job = job;
                }
                getName(){
                    return this.name;
                }
                getJob(){
                    return this.job;
                }
            }

            let goodGuy = new Person('Neo','the one');
            console.log(goodGuy);
```
## Inheritance
```javascript
            class superHero extends Person {
                constructor (name, heroName, superPower){
                    super(name);
                    this.heroName = heroName;
                    this.superHero = superPower;

                }
                secretIdentity(){
                    return`${this.heroName} is ${this.name}!!`

                }
            }
            let batman= new superHero("Bruce Wayne","Im Batman")
            console.log(batman.secretIdentity())
```
```javascript
            class Person{
                constructor (name){
                    this.name = name;

                }
                set name(name){
                    this._name=name;

                }
                get name(){
                    return this._name
                }
            }

            Let goodGuy = new Person ('Jim Gordon');
            console.log(goodGuy.name);
            goodGuy.name="James Gordon";
            console.log(goodGuy.name);
```
```javascript
            let student = {name:"Adam"};
            let status = new Map();
            status.set(student.name, "Adam");
            status.set("feeling","churlish");
            console.log(status.get(student.name));
            console.log(status.get("feeling"))
```   
    