# js.ax
Safety tips for working with JavaScript

A collection of tips to make your JavaScript code safe for you and others. 

## Contributing
Please feel free edit this file (README.md) and add your horror stories about bad JavaScript code. 

# Tips 

#### Pro Tip: separate and name your callbacks and bind them to avoid stagnant closure values

  new ES arrow functions make it even more tempting to write dangerous stuff like this:


**Potentially Broken Code:**

````

function bindMyAction(getSomeValue) {

  const  someValue = getSomeValue();
  myElement.addEventListener('click',(e)=>{
    myData.remove(someValue, e.target)
  });
  //someValue is always the same for all subsequent clicks.
  //Are you sure this is what you intended?
}


````

**Working code**
````
function removeData(e) {
  myData.remove(this.getSomeValue(),e.target)
}

function bindMyAction(getSomeValue) {
  const clickHandler = removeData.bind({getSomeValue});
  myElement.addEventListener('click',clickHandler);
}

````
