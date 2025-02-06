# AWS-Academy-Modules-Export
JS script to export Lab and Knowledge checks on AWS academy

## Why?

To track procress on excel since the grading page doesn't show lab progress anymore, I decifed to include `Knowledge Check` just because.

## Code
```js
let items = document.getElementById("context_modules").children

let kC = {};
let lab = {};

for(let tempItem of items){
    let moduleItems = tempItem.children[2].children[0].children;
    for (let mi2 of moduleItems) {
        let mi3 = mi2.children[0]?.getElementsByClassName("module-item-title")[0].children[0].children[0];
        let itemName = mi3?.textContent.trim();
        let itemUrl = mi3?.href;
        if (mi3 === undefined) {
            continue
        }
        if (itemName?.indexOf("Lab") !== -1){
             lab[itemName] = itemUrl;
        }
        if (itemName?.indexOf("Knowledge Check") !== -1) {
            kC[itemName] = itemUrl;
        }
    }
};

let combinded = { ...kC, ...lab}

//Excel Friendly output
let itemsList = []
for (const [key, value] of Object.entries(combinded)) {
  itemsList.push(key)
}
for (const [key, value] of Object.entries(combinded)) {
  itemsList.push(value);
}
console.log(itemsList.join("\n"));
```

## Useage

1. Open the module tab of the course you want to export 
2. Open developer console and goto the console
3. type in `allow pasting` to allow pasting cde into the console
4. Copy the code above and paste it into the console

## Output Example

```js
Module 2 Knowledge Check
Module 3 Knowledge Check
Module 4 Knowledge Check
https://awsacademy.instructure.com/courses/999999/modules/items/9999992
https://awsacademy.instructure.com/courses/999999/modules/items/9999993
https://awsacademy.instructure.com/courses/999999/modules/items/9999994
```

Top half is the item title and the bottiom half is the item url corrsponding to the item title like below
| Title | URL |
| - | - |
| Module 2 Knowledge Check | https://awsacademy.instructure.com/courses/999999/modules/items/9999992 |
| Module 3 Knowledge Check | https://awsacademy.instructure.com/courses/999999/modules/items/9999993 |
| Module 4 Knowledge Check | https://awsacademy.instructure.com/courses/999999/modules/items/9999994 |
